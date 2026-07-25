# Greedy

## Signal

Typically finding the minimum or the maximum of a property of the input array.

## Steps

1. Determine if you should greedily pick the minimum or the maximum at each step.
2. Sort the input array (often you may need to sort based on the frequency of each element using `Counter(<list>)`).
3. Iterate over the sorted array and increment the result, making use of a priority queue as needed.

