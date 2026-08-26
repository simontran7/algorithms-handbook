# Recursion

## Introduction

**Recursion** is an algorithmic paradigm in which a problem is solved by defining a solution in terms of smaller instances of the same problem.

We can implement a recursive algorithm by modelling it as a **recurrence relation**:
- **Base Case(s)**: A terminating condition that can be solved directly without making another recursive call.
- **Recursive Case**: A set of rules that reduces a problem to a smaller instance of the same problem, eventually leading to the base case.

Concretely, a recursive algorithm is typically implemented through a **function calling itself**. Specifically, each time a recursive function calls itself, it reduces the given problem into subproblems (the recursive case). The recursive calls should continue until it reaches a point where the subproblem can be solved without further recursing (the base case).

```
func recursive_algo(<state variables 1>, <state variable 2>, <...>, <state variable N>) {
    // base case(s)
    if <condition> {
        return <base case result>;
    }
    if <condition> {
        return <base case result>;
    }

    // recursive case
    <...>
    return recursive_algo(<...>);
}
```

## Examples

[Reverse String](https://leetcode.com/problems/reverse-string/description/)

[Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

## From Recursion to Iteration

...

## From Recursion to Tail Recursion 

In a traditional recursive function, calculations happen after the recursive call returns. In a **tail-recursive function**, the recursive call is the absolute *last* operation executed by the function. 

The tail-recursive function lends itself to better memory usage, as in certain languages that support **Tail Call Optimization**, the compiler automatically optimizes tail-recursive functions into loops under the hood. Specifically, instead of adding a new stack frame for every call, it continuously reuses the same stack frame (which stores the returning address of the function call, the arguments that are passed to the function call, and the local variables within the function call if any), preventing stack overflow errors. As a consequence, when the function recurses to the base case, the function can simply return the result to the original caller without going back to the previous function calls.

To turn a standard recursive function into a tail-recursive function, you pass the partial results forward using an **accumulator argument** so nothing is left to compute when the call returns. 

A **continuation**, often named `k`, is a stack of functions modelling the call stack, i.e. the work we still need to do upon returning.

1. Add the continuation higher order function as the accumulator argument. Then:
- **Base Case**: apply the continuation on the base case's result.
- **Recursive Case**: all the work that previously executed *after* the recursive call now gets moved inside the continuation

For recursive algorithms with different possible outcomes, we may introduce a **failure continuation** and a **success continuation**. The failure continuation specifies what to do when the computation fails, while the success continuation specifies what to do when it succeeds. When either outcome occurs, control is transferred to the corresponding continuation, which carries out the remaining computation and, in the case of success, helps produce the final result.

### Regular Continuation Examples

#### Example 1

```ocaml
let rec append l1 l2 =
  match l1 with
  | [] -> l2
  | h :: t -> h :: append t l2
;;
```

turned into 

```ocaml
let rec append_tr l1 l2 =
  let rec helper l1 l2 k =
    match l1 with
(* instead of returning the result `l2`, we apply the continuation `k` to `l2` *)
    | [] -> k l2
(* instead of constructing `h :: append t l2`, we call `append_tr` recursively on `t` and `l2`, adding the task of prepending `h` to the argument `r` of the continuation `k` *)
    | h :: t -> helper t l2 (fun r -> k (h :: r))
  in
  helper l1 l2 (fun r -> r)
;;
```

where for example, `append_tr [1; 2] [3; 4]` executes as follows:

```
append_tr [1; 2] [3; 4]
=> helper [1; 2] [3; 4] (fun r -> r)
=> helper [2] [3; 4] (fun r1 -> (fun r -> r) (1 :: r1))
=> helper [] [3; 4] (fun r2 -> (fun r1 -> (fun r -> r) (1 :: r1)) (2 :: r2))
=> (fun r2 -> (fun r1 -> (fun r -> r) (1 :: r1)) (2 :: r2)) [3; 4]
=> (fun r1 -> (fun r -> r) (1 :: r1)) (2 :: [3; 4]))
=> (fun r -> r) (1 :: 2 :: [3; 4]) 
=> (1 :: 2 :: [3; 4])
=> [1; 2; 3; 4]
```

#### Example 2

For a binary tree

```ocaml
type 'a tree =
  | Empty
  | Node of 'a tree * 'a * 'a tree
```

We have the traditional `find_all` recursive function

```ocaml
let rec find_all predicate tree =
  match tree with
  | Empty -> []
  | Node (left, value, right) ->
      if predicate value then
        (find_all predicate left) @ (value :: (find_all predicate right))
      else
        (find_all predicate left) @ (find_all predicate right)
```

turned into the tail-recursive function via CPS

```ocaml
let rec find_all_tr predicate tree =
  let rec helper predicate tree k =
    match tree with
    | Empty -> k []
    | Node (left, value, right) ->
        helper predicate left
          (fun left_results ->
            helper predicate right
              (fun right_results ->
                if predicate value then
                  k (left_results @ (value :: right_results))
                else
                  k (left_results @ right_results)))
  in
  helper predicate tree (fun results -> results)
```

or alternatively, turned into

```ocaml
let rec find_all_tr predicate tree =
  let rec helper predicate tree k =
    match tree with
    | Empty ->
        k []
    | Node (left, value, right) ->
        if predicate value then
          helper predicate left (fun left_results ->
            helper predicate right (fun right_results ->
              k (left_results @ (value :: right_results))))
        else
          helper predicate left (fun left_results ->
            helper predicate right (fun right_results ->
              k (left_results @ right_results)))
  in
  helper predicate tree (fun results -> results)
```

### Success and Failure Continuation Examples

#### Example 1

For the following binary tree:

```ocaml
type 'a tree =
  | Empty
  | Node of 'a tree * 'a * 'a tree
```

We have either

```ocaml
let rec find p t =
  match t with
  | Empty -> None
  | Node (l, d, r) ->
      if p d then Some d
      else
        match find p l with
        | Some d -> Some d
        | None -> find p r
```

or we have

```ocaml
exception Fail

let rec find_exc p t = match t with 
  | Empty -> raise Fail
  | Node (l,d,r) -> 
    if (p d) then Some d
    else (try find_exc p l with Fail -> find_exc p r)

let find_ex p t =  (try find_exc p t with Fail -> None)
```

```ocaml
let rec find_tr p t fail succeed = match t with 
  | Empty -> fail ()
  | Node(_, d, _) when p d -> succeed d
  | Node(l, _, r) ->
     find_tr p l (fun () -> find_tr p r fail succeed) succeed

let find_tr_opt p t = find_tr p t (fun () -> None) (fun x -> Some x)
let find_tr_exn p t =
  find_tr p t (fun () -> raise Fail) (fun x -> x)
```

#### Example 2

```ocaml
(**
  * -----------------------------------------------------------------
  * Let's make change with coins
  *
  * Given some list l of coin denominations and some amount n,
  * express n is terms of the coins l using the least amount of
  * coins.
  *
  * We assume that denominations are sorted in decreasing order,
  * e.g., [5; 2].
*)

(* It might not be possible to make change. *)
exception Change

(**
  * Examples:
  * # change [50;25;10;5;2;1] 43;;
  * - : int list = [25; 10; 5; 2; 1]
  * # change [50;25;10;5;2;1] 13;;
  * - : int list = [10; 2; 1]
  * # change [5;2;1] 13;;
  * - : int list = [5; 5; 2; 1]
  * The idea is to proceed greedily, but if we get stuck,
  * we undo the most recent greedy decision and proceed again from there.
  *
  * We implement three versions:
  * change_exn  : int list -> int -> int list
  * change_opt  : int list -> int -> int list option
  * change_cont : int list -> int -> (int list -> 'a) -> (unit -> 'a) -> 'a
*)

let rec change_exn coins amt =
  match coins with
  (* If the amount of change to make is zero, then we're done. *)
  | _ when amt = 0 -> []
  | [] ->
    (**
      * If we run out of available coins but amt is non-zero, then
      * fail with an exception to jump back to the nearest handler.
    *)
    raise Change
  | coin :: cs when coin > amt ->
    (**
      * If this coin is too large, then we forget about it for now
      * and consider the other coins.
    *)
    change_exn cs amt
  | coin :: cs ->
    try
      (**
        * Otherwise, we know that this coin is plausible, so we add
        * it to the return list and try to make change for the
        * remaining amount.
      *)
      coin :: change_exn coins (amt - coin)
    with
    | Change ->
      (**
        * It turns out that by using `coin` we were unable to make
        * the remaining change, so we forget about coin and try again
        * with the remaining coins.
      *)
      change_exn cs amt
```

```ocaml
let rec change_opt coins amt =
  match coins with
  | _ when amt = 0 -> Some []
  | [] -> None
  | coin :: cs when coin > amt -> change_opt cs amt
  | coin :: cs ->
    match change_opt coins (amt - coin) with
    | Some change -> Some (coin :: change)
    | None -> change_opt cs amt
```

and now turned into tail-recursive function

```ocaml
let rec change_cont coins amt s f =
  match coins with
  | _ when amt = 0 -> s []
  | [] -> f ()
  | coin :: cs when coin > amt -> change_cont cs amt s f
  | coin :: cs ->
    change_cont
      coins
      (amt - coin)
      (fun change -> s (coin :: change))
      (fun _ -> change_cont cs amt s f)

let change_cont_exn coins amt = change_cont coins amt (fun x -> x) (fun _ -> raise Change)
let change_cont_opt coins amt = change_cont coins amt (fun x -> Some x) (fun _ -> None)
```



