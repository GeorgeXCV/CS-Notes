# Grokking Algorithms
- [Big O](#big-o)
- [Recursion](#recursion)
- [Stack](#Stack)
- [Arrays](#arrays)
- [Linked Lists](#linked-lists)
- [Binary Search](#binary-search)
- [Selection sort](#selection-sort)

## Big O
Big O notation is special notation that tells you how fast an algorithm is. Big O doesn’t tell you the speed in seconds. Big O notation lets you compare the number of operations (n). It tells you how fast the algorithm grows. Big O notation is awalys about the worst-case scenario.

Here are ive Big O run times that you’ll encounter a lot, sorted from fastest to slowest:
• O(log n), also known as log time. Example: Binary search.
• O(n), also known as linear time. Example: Simple search.
• O(n* log n). Example: A fast sorting algorithm, like quicksort.
• O(n2). Example: A slow sorting algorithm, like selection sort. 
• O(n!). Example: A really slow algorithm, like the traveling salesperson.

## Recursion
Where a function calls itself. Recursion is used when it makes the solution clearer. There’s no performance beneit to using recursion; in fact, loops are sometimes better for performance. Loops may achieve a performance gain for your program. Recursion may achieve a performance gain for your programmer. Choose which is more important in your situation!

When you write a recursive function, you have to tell it when to stop recursing. That’s why every recursive function has two parts: the base case, and the recursive case. The recursive case is when the function calls itself. The base case is when the function doesn’t call itself again ... so it doesn’t go into an infinite loop.

```
def countdow n(i):  
  print i
  if i <= 0: // Base case    
    return
  else: // Recursive case    
    countdow n(i-1)
```

## Stack
When you insert an item, it gets added to the top of the list. When you read an item, you only read the topmost item, and it’s taken of the list. So your todo list has only two actions: push (insert) and pop (remove and read). 

Your computer uses a stack internally called the call stack. When you call a function from another function, the calling function is paused in a partially completed state.

All function calls go onto the call stack. The call stack can get very large, which takes up a lot of memory.

## Arrays
Each item is next to each other memory, great for when you want to access random elements as you can lookup any position instantly. 

Arrays offer faster reads.

## Linked Lists
Items can be anywhere in memory. Each item has address to next item in the list. Better than arrays for inserts since can don't have to worry about next memory being taken, can store anywhere.

Linked Lists are like Top 10 lists on websites, you can't go straight to the end as you don't know the location, you have go through it one by one.

Lists are better if you want to insert items into the middle. 

Lists are better if you want to delete, because you just need to change what the previous element points to. With arrays, everything needs to be moved up when you delete an element.

## Binary Search
Its input is a sorted list of elements. If an element you’re looking for is in that list, binary search returns the position where it’s located. 
Otherwise, binary search returns null. 

In general, for any list of n, binary search will take log2n steps to run in the worst case, whereas simple search will take n steps.

If the list is 100 items long, it takes at most 7 guesses. If the list is 4 billion items, it takes at most 32 guesses. 
Binary search runs in logarithmic time (log time).

## Selection Sort
You want to sort most played songs, you go through list, get most played item and add to new list, repeat for each song. To find the song with the highest play count, you have to check each item in the list. This takes O(n) time, as you just saw. So you have an operation that takes O(n) time, and you have to do that n times:

This takes O(n × n) time or O(n2) time.

Sorting algorithms are very useful. You can sort:
• Names in a phone book
• Travel dates
• Emails (newest to oldest)
