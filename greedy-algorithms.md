# Greedy Algorithms

## Use Case

A problem where:
- You want to maximize/minimize something
- You repeatedly have a choice of “what should I take/use/do next?”
- There is an obvious best choice at each step.
- You don't need to reconsider previous choices.
- Taking the best-looking option now doesn't make a future solution worse.

## Template

1. Determine if you should greedily pick the minimum or the maximum at each step.
2. Sort the input array as needed (often you may need to sort based on the frequency of each element).
3. Iterate over the sorted array and increment the result, making use of a priority queue as needed.

