# Grokking Algorithms
- [Binary Search](#binary-search)

## Binary Search
Its input is a sorted list of elements. If an element you’re looking for is in that list, binary search returns the position where it’s located. 
Otherwise, binary search returns null. 

In general, for any list of n, binary search will take log2n steps to run in the worst case, whereas simple search will take n steps.

If the list is 100 items long, it takes at most 7 guesses. If the list is 4 billion items, it takes at most 32 guesses. 
Binary search runs in logarithmic time (log time).
