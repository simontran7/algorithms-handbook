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

To turn a standard recursive function into a tail-recursive function, you must ensure that the recursive call is the absolute *last* operation executed by the function. 

In a traditional recursive function, calculations happen after the recursive call returns. In a tail-recursive function, you pass the partial results forward using an accumulator parameter so nothing is left to compute when the call returns. 

In languages that support **Tail Call Optimization**, the compiler automatically optimizes tail-recursive calls into loops under the hood. Instead of adding a new stack frame for every call, it continuously reuses the same stack frame, which prevents stack overflow errors.

A **continuation** is a stack of functions modelling the call stack, i.e. the work we still
need to do upon returning.

Add the continuation higher order function as the additional accumulator argument. Then:
- **Base Case**: call the continuation.
- **Recursive Case**: build up in the continuation the work to do after the recursive call.




