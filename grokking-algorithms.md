# Grokking Algorithms
- [Big O](#big-o)
- [Recursion](#recursion)
- [Stack](#Stack)
- [Arrays](#arrays)
- [Linked Lists](#linked-lists)
- [Hash Tables](#hash-tables)
- [Graphs](#graphs)
- [Binary Search](#binary-search)
- [Selection Sort](#selection-sort)
- [Divide & Conquer](#divide-&-conquer)
- [Quick Sort](#quick-sort)
- [Breadth-First Search](#breadth-first-search)

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

# Data Structures

## Arrays
Each item is next to each other memory, great for when you want to access random elements as you can lookup any position instantly. 

Arrays offer faster reads.

## Linked Lists
Items can be anywhere in memory. Each item has address to next item in the list. Better than arrays for inserts since can don't have to worry about next memory being taken, can store anywhere.

Linked Lists are like Top 10 lists on websites, you can't go straight to the end as you don't know the location, you have go through it one by one.

Lists are better if you want to insert items into the middle. 

Lists are better if you want to delete, because you just need to change what the previous element points to. With arrays, everything needs to be moved up when you delete an element.

## Hash Tables
Hash tables use an array for storage. A hash function is a function where you put in a string and you get back a number. It maps strings to numbers. You use them to make a Hash Table.

The hash function tells you exactly where the value is stored, so you don’t have to search at all! Put a hash function and an array together, and you get a data structure called a hash table.

They’re also known as hash maps, maps, dictionaries, and associative arrays.

Hash tables are great when you want to:
• Create a mapping from one thing to another thing e.g. Name and Phone Number
• Look something up
• Filter out duplicates

In the average case, hash tables take O(1) for everything. O(1) is called constant time. It means the time taken will stay the same, regardless of how  big the hash table is.

## Graphs
A graph models a set of connections. Gaphs are made up of nodes and edges (connection). A node can be directly connected to many other nodes. Those nodes are called its neighbors. Graphs are a way to model how diferent things are connected to one another. 

# Algorithims

## Binary Search
Its input is a sorted list of elements. If an element you’re looking for is in that list, binary search returns the position where it’s located. 
Otherwise, binary search returns null. 

In general, for any list of n, binary search will take log2n steps to run in the worst case, whereas simple search will take n steps.

If the list is 100 items long, it takes at most 7 guesses. If the list is 4 billion items, it takes at most 32 guesses. 
Binary search runs in logarithmic time (log time).

A hash table has keys and values. A hash table maps keys to values.

## Selection Sort
You want to sort most played songs, you go through list, get most played item and add to new list, repeat for each song. To find the song with the highest play count, you have to check each item in the list. This takes O(n) time, as you just saw. So you have an operation that takes O(n) time, and you have to do that n times:

This takes O(n × n) time or O(n2) time.

Sorting algorithms are very useful. You can sort:
• Names in a phone book
• Travel dates
• Emails (newest to oldest)

## Divide & Conquer
D&C algorithms are recursive algorithms. To solve a problem using D&C, there are two steps:
1. Figure out the base case. This should be the simplest possible case.
2. Divide or decrease your problem until it becomes the base case.

D&C works by breaking a problem down into smaller and smaller pieces. If you’re using D&C on a list, the base case is probably an empty array or an array with one element.

## Quick Sort
A sorting algorithm much faster than selection sort. If you’re implementing quicksort, choose a random element as the pivot. The average runtime of quicksort is O(n log n)!

## Breadth-first Search
Breadth-first search allows you to find the shortest path between two things. It could be the shortest route to your friend’s house. It could be the smallest number of moves to checkmate in a game of chess.

There are two steps:
1. Model the problem as a graph.
2. Solve the problem using breadth-first search.

Two questions that breadth-first search can answer for you:
• Question type 1: Is there a path from node A to node B? (Is there a mango seller in your network?)
• Question type 2: What is the shortest path from node A to node B? (Who is the closest mango seller?)
