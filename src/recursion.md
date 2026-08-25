# Recursion

## Tail Recursion

A **continuation** is a stack of functions modelling the call stack, i.e. the work we still
need to do upon returning.

Add an additional argument, a **continuation** which acts like an accumulator. Then:
- **Base Case**: call the continuation.
- **Recursive Case**: build up in the continuation the work to do after the recursive call.




