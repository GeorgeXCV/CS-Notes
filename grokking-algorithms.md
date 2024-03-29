# Grokking Algorithms
- [Big O](#big-o)
- [Recursion](#recursion)
- [Stack](#stack)
- [NP Complete](#np-complete)
- [Map Function](#Map)
- [Reduce Function](#Reduce)
- [Arrays](#arrays)
- [Linked Lists](#linked-lists)
- [Hash Tables](#hash-tables)
- [Graphs](#graphs)
- [Trees](#trees)
- [Binary Search](#binary-search)
- [Selection Sort](#selection-sort)
- [Divide & Conquer](#divide-&-conquer)
- [Quick Sort](#quick-sort)
- [Breadth-First Search](#breadth-first-search)
- [Dijkstra’s algorithm](#dijkstra’s-algorithm)
- [Greedy Algorithm](#greedy-algorithm)
- [Dynamic Programming](#dynamic-programming)
- [K-nearest Neighbors](#k-nearest-neighbors)
- [Bloom Filters](#bloom-filters)
- [HyperLogLog](#hyperloglog)

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

## NP Complete
Some problems are famously hard to solve e.g. Travelling Salesperson.

It’s nice to know if the problem you’re trying to solve is NP-complete. At that point, you can stop trying to solve it perfectly, and solve it using an approximation algorithm instead. 

It can be hard to tell if a problem is NP-complete. Usually there’s a very small diference between a problem that’s easy to solve and an NP-complete problem. No easy way to tell.

Here are some giveaways:
• Your algorithm runs quickly with a handful of items but really slows down with more items.
•  “All combinations of X” usually point to an NP-complete problem.
•  Do you have to calculate “every possible version” of X because you can’t break it down into smaller sub-problems? Might be  NP-complete.
•  If your problem involves a sequence (such as a sequence of cities, like traveling salesperson), and it’s hard to solve, it might be NP-complete.
•  If your problem involves a set (like a set of radio stations) and it’s hard to solve, it might be NP-complete.
•  Can you restate your problem as the set-covering problem or the traveling-salesperson problem? Then your problem is deinitely  NP-complete.

## Map
The map function is simple: it takes an array and applies the same function to each item in the array. 

## Reduce
The idea is that you “reduce” a whole list of items down to one item. With map, you go from one array to another. With reduce, you transform an array to a single item.

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

## Trees
For every node, the nodes to its let are smaller in value, and the nodes to the right are larger in value. 

Searching for an element in a binary search tree takes O(log n) time on average and O(n) time in the worst case. 

A binary search tree is a lot faster for insertions and deletions on average. But you don't get random access.

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

Breadth-irst search is used to calculate the shortest path for an unweighted graph.

## Dijkstra’s algorithm
Shortest path is not necessarily the fastest, this finds the fastest.

There are four steps to Dijkstra’s algorithm:
1. Find the “cheapest” node. This is the node you can get to in the least amount of time.
2. Check whether there’s a cheaper path to the neighbors of this node. If so, update their costs.
3. Repeat until you’ve done this for every node in the graph.
4. Calculate the final path.

When you work with Dijkstra’s algorithm, each edge in the graph has a number associated with it. These are called weights.

A graph with weights is called a weighted graph. A graph without weights is called an unweighted graph.

Dijkstra’s algorithm is used to calculate the shortest path for a weighted graph.

## Greedy Algorithm
A greedy algorithm is simple: at each step, pick the optimal move. In this case, each time you pick a class, you pick the class that ends the soonest. In technical terms: at each step you pick the locally optimal solution, and in the end you’re left with the globally optimal solution.

Obviously, greedy algorithms don’t always work. But they’re simple to write! 

Sometimes, perfect is the enemy of good. Sometimes all you need is an algorithm that solves the problem pretty well. And that’s where greedy algorithms shine, because they’re simple to write and usually get pretty close.

## Dynamic Programming
Dynamic programming starts by solving subproblems and builds up to solving the big problem.

Every dynamic-programming algorithm starts with a grid. 

Dynamic programming is powerful because it can solve subproblems and use those answers to solve the big problem. Dynamic programming only works when each subproblem is discrete—when it doesn’t depend on other subproblems.

Dynamic programming is useful when you’re trying to optimize something given a constraint. 

## K-nearest Neighbors
The KNN algorithm is simple but useful! If you’re trying to classify something, you might want to try KNN first. 

Suppose you’re Netlix, and you want to build a movie recommendations system for your users. 

You can plot every user on a graph. These users are plotted by similarity, so users with similar taste are plotted closer together. Suppose you want to recommend movies for Sarah. Find the five users closest to her.

Once you have this graph, building a recommendations system is easy. If X likes a movie, recommend it to Sarah.

Suppose you’re comparing Netlix users, instead. You need some way to graph the users. So, you need to convert each user to a set of coordinates, just as you did for fruit.

Once you can graph users, you can measure the distance between them. Here’s how you can convert users into a set of numbers. When users sign up for Netlix, have them rate some categories of movies based on how much they like those categories. For each user, you now have a set of ratings!

These are the two basic things you’ll do with KNN—classiication and regression:
• Classiication = categorization into a group
• Regression = predicting a response (like a number)

## Bloom Filters
Suppose you’re running Reddit. When someone posts a link, you want to see if it’s been posted before. Stories that haven’t been posted before are considered more valuable. So you need to igure out whether this link has been posted before.

Hash tables work but no good if the data set is very large.

Bloom filters ofer a solution. Bloom filters are probabilistic data structures. They give you an answer that could be wrong but is probably correct. Instead of a hash, you can ask your bloom filter if you’ve crawled this URL before. A hash table would give you an accurate answer. A bloom filter will give you an answer that’s probably correct.

Bloom filters are great because they take up very little space. A hash table would have to store every URL crawled by Google, but a bloom filter doesn’t have to do that. They’re great when you don’t need an exact answer.

## HyperLogLog
Along the same lines is another algorithm called HyperLogLog. Suppose Google wants to count the number of unique searches performed by its users. Or suppose Amazon wants to count the number of unique items that users looked at today. Answering these questions takes a lot of space! With Google, you’d have to keep a log of all the unique searches. When a user searches for something, you have to see whether it’s already in the log. If not, you have to add it to the log. Even for a single day, this log would be massive! 

HyperLogLog approximates the number of unique elements in a set. Just like bloom filters, it won’t give you an exact answer, but it comes very close and uses only a fraction of the memory a task like this would otherwise take.
