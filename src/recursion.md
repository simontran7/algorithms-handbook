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

A **continuation** is a stack of functions modelling the call stack, i.e. the work we still need to do upon returning.

1. Add the continuation higher order function as the accumulator argument. Then:
- **Base Case**: apply the continuation on the base case's result.
- **Recursive Case**: all the work that previously executed *after* the recursive call now gets moved inside the continuation

### Examples

#### Example 1

```ocaml
let rec append l1 l2 =
  match l1 with
  | [] -> l2
  | h :: t -> h :: append t l2
;;

let rec append_tr l1 l2 =
  let rec helper l1 l2 acc =
    match l1 with
(* instead of returning the result `l2`, we apply the continuation `cont` to `l2` *)
    | [] -> acc l2
(* instead of constructing `h :: append t l2`, we call `append_tr` recursively on `t` and `l2`, adding the task of prepending `h` to the argument `r` of the continuation `cont` *)
    | h :: t -> helper t l2 (fun r -> acc (h :: r))
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


```ocaml
let rec findAll p t = match t with 
  | Empty -> []
  | Node(l,d,r) -> 
    if (p d) then (findAll p l) @(d ::(findAll p r))
    else
      (findAll p l) @ (findAll p r)
```

```ocaml
let rec findAll' p t sc = match t with 
  | Empty -> sc []
  | Node(l,d,r) -> 
    findAll' p l 
      (fun el ->
        findAll' p r
          (fun er ->
            if (p d) then sc (el@(d::er)) else sc (el@er)))

let rec findAll0 p t sc = match t with 
  | Empty -> sc []
  | Node(l,d,r) -> 
     (if (p d) then
       findAll0 p l (fun el -> findAll0 p r 
					(fun er ->  sc (el@(d::er)))) 
     else 
       findAll0 p l (fun el -> findAll0 p r 
					(fun er ->  sc (el@er))) 

     )
```

#### Example 3

```ocaml
type 'a tree =
  | Empty
  | Node of 'a tree * 'a * 'a tree
;;
```

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
;;
```

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

(** A driver function that calls the continuation-passing style
    function and wraps the result in an option, so we could use
    pattern matching after.
 *)
let find' p t = find_tr p t (fun () -> None) (fun x -> Some x)
```


