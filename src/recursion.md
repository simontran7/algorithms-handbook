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

To turn a standard recursive function into a tail-recursive function, there are two common approaches:
- **Accumulator**: Pass partial results forward using an accumulator argument, so there is no remaining work to perform after the recursive call returns.
- **Continuation (CPS)**: Pass the remaining work forward using a continuation, often named k. The continuation is a function that represents the work still to be performed and effectively models the pending computations of the call stack.

### Accumulator

1. Add an accumulator argument, usually named `acc`, to the recursive helper function.
2. Initialize the accumulator with the result corresponding to the base case.
3. Base case: Return the accumulator instead of returning the original base-case result.
4. Recursive case: Update the accumulator with the work that would have been performed after the recursive call.
5. Make the recursive call the final operation. 

#### Example 

```ocaml
let rec sum l =
  match l with
  | [] -> 0
  | h :: t -> h + sum t
```

turned into

```ocaml
let sum_tr l =
  let rec helper l acc =
    match l with
    | [] -> acc
    | h :: t -> helper t (acc + h)
  in
  helper l 0
```

### CPS 

1. Add a continuation higher-order function, usually named `k`, as an additional argument. 
2. Base case: Apply `k` to the base case's result.
3. Recursive case: Move all the work that previously happened after the recursive call into the continuation.
4. Make the recursive call the final operation.

#### Example 1

```ocaml
let rec append l1 l2 =
  match l1 with
  | [] -> l2
  | h :: t -> h :: append t l2
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

