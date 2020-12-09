# Grokking Algorithms
- [Binary Search](#binary-search)
- [Big](#big-o)

## Binary Search
Its input is a sorted list of elements. If an element you’re looking for is in that list, binary search returns the position where it’s located. 
Otherwise, binary search returns null. 

In general, for any list of n, binary search will take log2n steps to run in the worst case, whereas simple search will take n steps.

If the list is 100 items long, it takes at most 7 guesses. If the list is 4 billion items, it takes at most 32 guesses. 
Binary search runs in logarithmic time (log time).

## Big O
Big O notation is special notation that tells you how fast an algorithm is. Big O doesn’t tell you the speed in seconds. Big O notation lets you compare the number of operations (n). It tells you how fast the algorithm grows. Big O notation is awalys about the worst-case scenario.

Here are ive Big O run times that you’ll encounter a lot, sorted from fastest to slowest:
• O(log n), also known as log time. Example: Binary search.
• O(n), also known as linear time. Example: Simple search.
• O(n* log n). Example: A fast sorting algorithm, like quicksort.
• O(n2). Example: A slow sorting algorithm, like selection sort. 
• O(n!). Example: A really slow algorithm, like the traveling salesperson.

## Arrays
Each item is next to each other memory, great for when you want to access random elements as you can lookup any position instantly.


## Linked Lists
Items can be anywhere in memory. Each item has address to next item in the list. Better than arrays for inserts since can don't have to worry about next memory being taken, can store anywhere.

Linked Lists are like Top 10 lists on websites, you can't go straight to the end as you don't know the location, you have go through it one by one.

Lists are better if you want to insert items into the middle. 

Lists are better if you want to delete, because you just need to change what the previous element points to. With arrays, everything needs to be moved up when you delete an element.
