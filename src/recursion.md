# Recursion

## Tail Recursion 

To turn a standard recursive function into a tail-recursive function, you must ensure that the recursive call is the absolute *last* operation executed by the function. 

In a traditional recursive function, calculations happen after the recursive call returns. In a tail-recursive function, you pass the partial results forward using an accumulator parameter so nothing is left to compute when the call returns. 

In languages that support **Tail Call Optimization**, the compiler automatically optimizes tail-recursive calls into loops under the hood. Instead of adding a new stack frame for every call, it continuously reuses the same stack frame, which prevents stack overflow errors.

A **continuation** is a stack of functions modelling the call stack, i.e. the work we still
need to do upon returning.

Add the continuation higher order function as the additional accumulator argument. Then:
- **Base Case**: call the continuation.
- **Recursive Case**: build up in the continuation the work to do after the recursive call.




