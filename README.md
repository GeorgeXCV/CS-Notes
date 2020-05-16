# Computer Science
## Big O
Big O is the way we analyze how efficient algorithms. We can model how much time any function is going to take given n inputs, but in reality we're interested in the order of magnitude of the number and necessarily of the exact figure.
Only care about huge difference, if function is 300ms vs 330 ms, whatever. But 500ms vs 30 seconds is huge. We ignore the little parts and concentrate on the big parts.

With 3x² + x + 1, the Big O for this equation would be O(n²) where O is just absorbing all the other fluff (including the factor on the biggest term.) Just grab the biggest term. So for n terms, it's going take us n*n time to go through our inputs. 

 This is O(n) because we go through all the inputs once in a loop. 
```
function crossAdd(input) {
    var answer = [];
    for (var i = 0; i < input.length; i++) {
        var goingUp = input[i];
        var goingDown = input[input.length-1-i];
        answer.push(goingUp + goingDown);
    }
    return answer;
}
```

 This would be O(n²). For every input, we have to go through a full loop inside of another full loop, meaning we're doing a lot of work! This is the trick: look for loops. A loop inside of a loop inside of a loop would likewise be O(n³).

If we have no loops and just do something and exit/return, then it's said we're doing it in constant time, or O(1). 
```
function makeTuples(input) {
    var answer = [];
    for (var i = 0; i < input.length; i++) {
        for (var j = 0; j < input.length; j++) {
            answer.push([input[i], input[j]]);
        }
    }
    return answer;
}
```
## Recursion
Recursion is when you define something in terms of itself.

When we talk about recursion in computer science, we are talking about a function that calls itself. This technique is especially adept at some problems because of its ability to maintain state at different levels of recursion.

While recursion can make the code very simple for some problems, it inherently carries a potentially large footprint with it as every time you call the function, it adds another call to the stack. Some problems therefore are better solved in a slightly-more-complicated-but-more-effecient way of iteration (loops) instead of recursion. 

Function that computes a factorial recursively: 
```
function factorial(num) {
  if (num < 2) return 1;
  return num * factorial(num-1);
}
```
A factorial is when you take a number n and multiply by each preceding integer until you hit one.

## Sorting Algorithms
### Bubble Sort
One straight line, easiest to conceptualize and a natural way for the brain to think about sorting so it's typical to do bubble sort first. It's also amongst the least efficient in terms of worst case scenario. 

Loop through the array and compare each index with the index next to it. If the those two numbers are out of order (the lesser index's value is greater than the greater index's value) we swap those two numbers' places in the array. We keep looping over that array until everything is in place and nothing was swapped during the last iteration. 

What's the Big O? Well, there's an inner loop to check to see if indexes need to be swapped, and an outer loop that's just checking to see if anything was swapped. That would be make it O(n²). Not efficient, but a great learning tool. You'll never use bubble sort for anything serious. 

```
var bubbleSort = nums => {  
  do {
    var swapped = false;
    for (var i = 0; i < nums.length; i++) {
      snapshot(nums);
      if (nums[i] > nums[i+1]) {
        var temp = nums[i];
        nums[i] = nums[i+1];
        nums[i+1] = temp;
        swapped = true;
      }
    }
  } while(swapped);
  snapshot(nums);
};
```

### Insertion Sort
Insertion sort is a step more complex but a bit more useful than bubble sort and is occasionally useful. The worst case scenario for it is similar to bubble sort's but its best case makes it suited for times when you're pretty sure a list almost sorted or likely already sorted. 

We're going to start at the beginning of the list and assume we have a sorted list of length 1 where the first element is only sorted element. We're then going to grab the second element, and insert it into the correct spot in our sorted list, either the 0 index or the 1 index, depending if it's smaller or larger than our first element. We now have a sorted list of length 2. We then continue on down the line, inserting elements in our sorted side of the list as the unsorted side dwindles. 

What's the Big O? There's an inner loop that goes over your sorted list to find the correct place to insert your item, and an outer loop to go over all the numbers. Two loops means O(n²). However since if your list is sorted or nearly so, it can be O(n) in a best case scenario and thus well adapted to that scenario.

```
var insertionSort = nums => {  
  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      snapshot(nums);
      if (nums[i] < nums[j]) {
        let spliced = nums.splice(i, 1);
        nums.splice(j, 0, spliced[0]);
      }
    }
  }
};
```

### Merge Sort
Merge sort is actually very useful and one of the easier divide-and-conquer algorithms to understand. A key to merge sort is that it is recursive. Take a big list, and first divide down in two half size lists and recursively call merge sort on those smaller list, which in turn will do the same. The base case is when you have a list of one, at which point you will return that sorted list of one. On the way up the recursive calls, you will merge those sorted lists together (preferably by another merge function you'll write) that walks through both lists simultaneously and inserts the smaller value first, effectively creating a bigger sorted list. 

```
[1, 5, 6] sublist 1
[2, 7, 8] sublist 2

-> compare 1 and 2, take 1 and put it in new list
-> compare 5 and 2, take 2 and put it in new list
-> compare 5 and 7, take 5 and put it in new list
-> compare 6 and 7, take 6 and put it in new list
-> list one has no more elements
   add the rest of list two in order (7 and 8)
```

This combined merge with the divide-and-conquer recursion proves to be pretty effective. When you call Array.prototype.sort it often uses MergeSort (depending on the engine and the types of the elements in the array.) MergeSort is also stable which just means if you have equivalent elements, it will keep their original order in the array. This is sometimes important and sometimes not. 

Big O is O(n log n). We compare everything once, but we don't have to compare everything to everything like we do with bubble sort. Rather we just to have to compare to their local lists as we sort. Not too bad.

MergeSort's space complexity is a bit worse than the previous algorithms at O(n) since we have to create new lists as we go. It's not awful but it nonetheless a consideration. 

```
const mergeSort = nums => {
  if (nums.length < 2) {
    return nums;
  }
  const length = nums.length;
  const middle = Math.floor(length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);
  
  return merge(mergeSort(left), mergeSort(right));
};

const merge = (left, right) => {
  
  const results = [];
  
  while (left.length && right.length) {
    
    if (left[0] <= right[0]) {
      results.push(left.shift());
    }
    else {
      results.push(right.shift());
    }
  }
  
  return results.concat(left, right);
};

```

### Quick Sort
Quicksort is one of the most useful and powerful sorting algorithms out there, and it's not terribly difficult to conceptualize. Occasionally JavaScript doesn't mergesort for Array.prototype.sort. In those other cases, it's usually some variant on quicksort.

It's another divide-and-conquer, recursive algorithm but it takes a slightly different approach. The basic gist is that you take the last element in the list and call that the pivot. Everything that's smaller than the pivot gets put into a "left" list and everything that's greater get's put in a "right" list. You then call quick sort on the left and right lists independently (hence the recursion.) After those two sorts come back, you concatenate the sorted left list, the pivot, and then the right list (in that order.) The base case is when you have a list of length 1 or 0, where you just return the list given to you. 
```
[4,9,3,5] list
-> 5 is made the pivot since it's the last in the array
-> divide list into two lists, [4,3] and [9]
-> call quicksort on those two lists

[4, 3]
-> 3 is pivot
-> call quicksort on [] and [4]
-> those both return as is as they are the base case of length 0 or 1
-> concat [], 3, and [4]
-> return [3,4]

[9]
-> returns as this it is a base case of length 1

(back into the original function call)
-> call concat on [3,4], 5, and [9]
-> return [3,4,5,9]
```

Another Big O of O(n log n) but takes up less memory than mergesort so it is often favored. However it does really poorly if you pass it a sorted list. It would always have a pivot of the biggest number which defeats the effectiveness of the divide-and-conquer approach as one side will always contain all the elements. Hence not good for lists you expect may already be sorted. There are some tricks to employ to get around that like checking the beginning, middle, and end numbers and swapping them to try to get the best pivot. There are a lot of subtle variants on quicksort. 
```
const quickSort = nums => {
  if (nums.length <= 1) return nums;
  
  const pivot = nums[nums.length-1];
  const left = [];
  const right = [];
  
  for (let i = 0; i < nums.length-1; i++) {
    if (nums[i] < pivot) {
      left.push(nums[i]);
    }
    else {
      right.push(nums[i]);
    }
  }
  return [...quickSort(left), pivot, ...quickSort(right)];
};
```

## Data Structures - Interfaces
### Set
Also known as Collections depending which language you're working with. A set allows allows at least four things: add, remove, contains, and toList. The basic idea is that you can add items to a set and then later check if they're there. You can also request later a list of those items in the set (though with no guaranteed order; sets have no notion of order.) They're also useful for deduplication since you can only add something to a set once. 

### Map
Maps are quite similar to simple JavaScript objects. Maps are a set/collection of keys that have values associated with those keys. Unlike objects, they don't have prototypes, inheritance, methods, or anything of that sort. Maps are also similar to associative arrays in other languages. Again, since the keys are a set, there cannot be duplication of keys. You can have duplication of values though. Key 'thing' can have value 'map' while key 'other thing' can have a value of 'map' as well. 

### Stack
Stack is an interface that adheres to the "Last-In First-Out" (LIFO) mantra. In a stack, you can only push (add) or pop (remove.) The last thing you pushed will be what pop returns to you (pop will also remove it from the stack.) Often they'll have a method called peek too which just looks at the top value of the stack without modifying the stack. 

Example Function:
```
function double(x) { return 2 * x; }
function squareAndAddFive(y) { return square(y) + 5; }
function square(z) { return z * z; }

function maths(num) {
    var answer = double(num);
    answer = squareAndAddFive(answer);
    return answer;
}

maths(5);
```

How it works:
```
-> maths is called; JS pushes maths call on its call stack
-> inside maths, double is called; JS pushes double onto its call stack
-> doubles completes, returns value 10; JS pops double off its call stack
-> back inside maths, squareAndAddFive is called;
   JS pushes squareAndAddFive on its call stack
-> inside squareAndAddFive, square is called;
   JS pushes square on its call stack

Let's look at call stack right now

square
squareAndAddFive
maths
main

-> square completes, returns 100
-> squareAndAddFive completes, returns 105
-> maths completes, returns 105
```

### Queue
Queues adhere to the "First-In First-Out" mantra. All stacks need to have the methods enqueue (add/push) and dequeue (remove/pop). Like stacks, they'll have peek to see what the next element is to dequeue. 

Queues are useful for lots of programming problems. How about print jobs? Usually you want things to print in the order sent to the printer; otherwise Janice from Accounting is going to be printing all of her documents before you can print anything.

There are also priority queues as well. In a priority queue you also assign a priority to the elements that are enqueued. Items that have higher priorities get dequeued first. This is useful for networking; some packets are more important than others. If you're streaming video, that gets a high priority because getting a packet later means likely skipping some frames, whereas syncing to Dropbox can wait for a lull in network traffic to continue syncing. 

## Data Structures - Implementations
### Array List
ArrayList is done by directly interacting with an allocated piece of memory. You then interact with that allocated piece of memory by addressing the specific indices in the array. In other words, you just treat it like a normal array. However things get a bit more complicated when deleting items from an ArrayList: you have to collapse the list down to the spot where you deleted. 
```
[a,b,c,d,e,f,g]
-> delete index 3
-> array is [a,b,c,(blank),e,f,g]
-> shift elements 4,5,6 back one index
-> array is [a,b,c,e,f,g]
-> decrement length
```

```
class ArrayList {
  constructor() {
    this.length = 0;
    this.data = {};
  }
  push(value) {
    this.data[this.length] = value;
    this.length++;
  }
  pop() {
    const ans = this.data[this.length-1];
    delete this.data[this.length-1];
    this.length--;
    return ans;
  }
  get(index) {
    return this.data[index];
  }
  delete(index) {
    const ans = this.data[index];
    this._collapseTo(index);
    return ans;
  }
  _collapseTo(index) {
    for (let i = index; i < this.length; i++) {
      this.data[i] = this.data[i+1];
    }
    delete this.data[this.length-1];
    this.length--;
  }
  serialize() {
    return this.data;
  }
}
```

### Linked List
Linked List is made of a bunch of nodes that point to the next one in the list. Every node in a Linked Lists has two properties, the value of whatever is being store and a pointer to the next node in the list. 

LinkedLists have their ups and downs. On one hand, adding and removing is a breeze: you just have the change the next pointer on the previous node and that's it. Getting is a pain though: if .get is called you have to loop through the nodes until you get to the right node. And that's the tradeoff between LinkedList and ArrayList: LinkedList's adds and deletes are O(1) but the gets are O(n); ArrayList's adds and deletes are O(n) but the gets are O(1). If you're doing a bunch of adds and deletes but not many gets, stick to LinkedLists. Doing a bunch of gets? ArrayLists. Both? You decide! 

Example of delete:
```
value: [a]   [b]   [c]   [d]
next:  [ ]-> [ ]-> [ ]-> [ ]-> null
```

```
-> delete is called on index 2 (value 'c')
-> grab the head (value 'a')
-> loop through the nexts until you get the index
   before the one to be deleted (value 'b')
-> change the the next of index 1 to be the next of index 2
-> decrement length
-> return the value of the deleted node
```

```
class LinkedList {
  constructor() {
    this.tail = this.head = null;
    this.length = 0;
  }
  push(value) {
    const node = new Node(value);
    this.length++;
    if (!this.head) {
     this.head = node;
    }
    else {
      this.tail.next = node;
    }
    this.tail = node;
  }
  pop() {
    if (!this.head) return null;
    if (this.head === this.tail) {
      const node = this.head;
      this.head = this.tail = null;
      return node.value;
    }
    const penultimate = this._find(null, (value, nodeValue, i, current) => current.next === this.tail );
    const ans = penultimate.next.value;
    penultimate.next = null;
    this.tail = penultimate;
    this.length--;
    return ans;
  }
  _find(value, test=this.test) {
    let current = this.head;
    let i = 0;
    while(current) {
      if (test(value, current.value, i, current)) {
        return current;
      }
      current = current.next;
      i++;
    }
    return null;
  }
  get(index) {
    const node = this._find(index, this.testIndex);
    if (!node) return null;
    return node.value;
  }
  delete(index) {
    if (index === 0) {
      const head = this.head;
      if (head) {
        this.head = head.next;
      }
      else {
        this.head = null;
      }
      this.length--;
      return head.value;
    }
    
    const node = this._find(index-1, this.testIndex);
    const excise = node.next;
    if (!excise) return null;    
    node.next = excise.next;    
    if (!node.next.next) this.tail = node.next;
    this.length--;
    return excise.value;
  }
  test(search, nodeValue) {
    return search === nodeValue;
  }
  testIndex(search, __, i) {
    return search === i;
  }
  serialize() {
    const ans = [];
    let current = this.head;
    if (!current) return ans;
    while (current) {
      ans.push(current.value);
      current = current.next;
    }
    return ans;
  }
}



class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

### Binary Search Tree
Trees cans be a useful structure for a middle ground between LinkedLists and ArrayLists. The gist of the BST is that a node in a BST has zero, one, or two subtrees. Every element in the left subtree is lesser than the value of the node and every node in the right is greater. By being able to depend on this fact, it makes it very simple to add and find new elements. Like LinkedLists, we just have to change pointers when we add new elements. 

Example:
```
Current Tree:
      10
    /   \
  5      15
 / \     /
3   8   12

-> .add is called with 7
-> start at root (10)
-> lesser than 10, go left to 5
-> greater than 5, go right to 8
-> lesser than 8, go left
-> no element at left, create new node
   and make it the left subtree of 8

         10
       /   \
     5      15
    / \     /
   3   8   12
      /
     7
```

BSTs get an average case of O(log n) on gets, adds, and deletes, but they can have a worst case of O(n) if you do something like add a sorted list to a BST. BSTs do perform well so long as you stay away from their edge cases. 
```
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (this.root === null) {
      this.root = new Node(value);
    }
    else {
      let current = this.root;
      while(true) {
        if (current.value > value) {
          // go left
          
          if (current.left) {
            current = current.left;
          }
          else {
            current.left = new Node(value);
            break;
          }
        }
        else {
          // go right
          if (current.right) {
            current = current.right;
          }
          else {
            current.right = new Node(value);
            break;
          }    
        }
      }
    }
    return this;
  }
  toJSON() {
    return JSON.stringify(this.root.serialize(), null, 4);
  }
  toObject() {
    return this.root.serialize();
  }
}

class Node {
  constructor(value=null, left=null, right=null) {
    this.left = left;
    this.right = right;
    this.value = value;
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    return ans;
  }
}
```

### AVL Tree
AVL tree are the answer to the problem that BST have: BST can easily get out of balance. Even if it's not the worst case scenario of ascending or descending lists being added, even a random distribution on numbers on a BST is going to pretty heavy in places. There are several ways to balance these trees.

AVLs are specialized BSTs. That is to say a valid AVL tree is always a valid BST (but not necessarily vice versa.) When you add a new value to a AVL tree, you do it the same way. The only difference is on the way up your recursive calls you check to see if the node is balanced after you added the new node. A tree is out of balance if its subtrees' difference of heights is greater than one. 

We can now guarantee that we won't hit those bad or worst case scenarios of having greatly out-of-balance trees and guarantee we won't hit the O(n) cases. Our worst case becomes O(log n). 

The basic idea is that if one side of tree gets too heavy (ie the max height of one of its children is two more than the max height of the other child) then we need to perform a rotation to get the tree back in balance. Let's take a look at the most basic rotation. 
```
5
 \
  8

-> Currently valid AVL tree
-> .add called with 9

5 - node A
 \
  8 - node B
   \
    9 - node C

(on the way up from the recursion)
-> check balance of node C: left height is 0, right height is 0, balanced
-> check balance of node B: left height is 0, right height is 1, balanced
-> check balance of node A: left height is 0, right height is 2
   unbalanced, right heavy, child is right heavy

-> perform right rotation
-> swap the values of nodes A and B
-> make node B the left child of node A
-> make node C the right child of node A
-> move node B's right child to its left child
   (in this case they're both null)
-> make node A's _original_ left child
   (which was null in this case) the left child of node B
-> update the heights of all the nodes involved

      8 - node A
   /     \
  5        9
node B   node C
```

This was a right rotation, but a left rotation is mirror of this. This generalized formula works for all but one case which we'll examine now. Even in this special case, all you have to do is perform an extra rotation which you already have the logic for. 

```
5
 \
  8

-> currently valid AVL tree
-> .add called with 7

5 - node A
 \
  8 - node B
 /
7 - node C


(on the way up from the recursion)
-> check balance of node C: left height is 0, right height is 0, balanced
-> check balance of node B: left height is 0, right height is 1, balanced
-> check balance of node A: left height is 0, right height is 2,
   unbalanced, right heavy, child is left heavy
```

You perform a double rotation when the opposite child is heavy during a rotation. Look at our example (the 5\8/7 example.) We're doing a right rotation but the left child of the right child is heavy (it's not out of balance, it's just heavier than the right child.) So what we're going to do is before we do a left rotation on the right child before we do a right rotation on the root node of the rotation. 

```
5 - node A
 \
  8 - node B
 /
7 - node C

[ ... previous steps ]
-> check balance of node A: left height is 0, right height is 2
   unbalanced - right heavy, child is left heavy
-> perform left rotation on left heavy right child node B

5 - node A
 \
  7 - node B
   \
    8 - node C

-> now perform right rotation on node A

      7 - node A
   /     \
  5        8
  node B   node C
 ```
  
Nailing down the logic of those rotations is a pain but once you do AVL trees are just a series of either left or right rotations on a BST. Even deletes follow this pattern; it's just in deletes sometimes you have to do even more rotations. 
 ```
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (!this.root) {
      this.root = new Node(value);
    }
    else {
      this.root.add(value);
    }
  }
  toJSON() {
    return JSON.stringify(this.root.serialize(), null, 4);
  }
  toObject() {
    return this.root.serialize();
  }
}

class Node {
  constructor(value=null, left=null, right=null) {
    this.left = left;
    this.right = right;
    this.value = value;
    this.height = 1;
  }
  add(value) {
    
    if (value < this.value) {
      // go left
      
      if (this.left) {
        this.left.add(value);
      }
      else {
        this.left = new Node(value);
      }
      if (!this.right || this.right.height < this.left.height) {
        this.height = this.left.height + 1;
      }      
    }
    else {
      // go right
      
      if (this.right) {
        this.right.add(value);
      }
      else {
        this.right = new Node(value);
      }
      if (!this.left || this.right.height > this.left.height) {
        this.height = this.right.height + 1;
      } 
    }
    this.balance();
  }
  balance() {
    const rightHeight = (this.right) ? this.right.height : 0;
    const leftHeight = (this.left) ? this.left.height : 0;
    
    console.log( this.value, leftHeight, rightHeight );
    
    if ( leftHeight > rightHeight + 1 ) {
      const leftRightHeight = (this.left.right) ? this.left.right.height : 0;
      const leftLeftHeight = (this.left.left) ? this.left.left.height : 0;
      
      if (leftRightHeight > leftLeftHeight) {
        this.left.rotateRR();
      }
      
      this.rotateLL();
    }
    else if ( rightHeight > leftHeight + 1 ) {
      const rightRightHeight = (this.right.right) ? this.right.right.height : 0;
      const rightLeftHeight = (this.right.left) ? this.right.left.height : 0;
      
      if (rightLeftHeight > rightRightHeight) {
        this.right.rotateLL();
      }
      
      this.rotateRR();
    }
  }
  rotateRR() {
    const valueBefore = this.value;
    const leftBefore = this.left;
    this.value = this.right.value;
    this.left = this.right;
    this.right = this.right.right;
    this.left.right = this.left.left;
    this.left.left = leftBefore;
    this.left.value = valueBefore;
    this.left.updateInNewLocation();
    this.updateInNewLocation();
  }
  rotateLL() {
    const valueBefore = this.value;
    const rightBefore = this.right;
    this.value = this.left.value;
    this.right = this.left;
    this.left = this.left.left;
    this.right.left = this.right.right;
    this.right.right = rightBefore;
    this.right.value = valueBefore;
    this.right.updateInNewLocation();
    this.updateInNewLocation();
  }
  updateInNewLocation() {
    if (!this.right && !this.left) {
      this.height = 1;
    }
    else if (!this.right || (this.left && this.right.height < this.left.height)) {
        this.height = this.left.height + 1;
    }
    else { //if (!this.left || this.right.height > this.left.height)
        this.height = this.right.height + 1;
    }
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    ans.height = this.height;
    return ans;
  }
}
 ```
 
### Hash Table
Hash tables are extremely powerful tools in modern CS and are used extensively in things like programming languages' underpinnings, databases, caches, etc. They do have some tradeoffs, namely potentially memory footprints and the need for complicated hashing but they have constant time (O(1)) lookups, deletes, and adds if you're doing a set or map. 

The gist of a hash table is you send your key through a hashing function (like MD5, SHA1, or one of your invention) which converts the to an addressable space (some sort of index.) Since in JavaScript we don't actually manage memory on that low of level, we're going to approximate the way it would work with a large empty array. However keep in mind that if this was a language where we managed our own memory we'd be doing that instead. 

This is powerful for maps because now our key points to exactly where our object is being store. And it's very powerful for sets because we can just check where if anything exists that memory address and if so then it exists; if not then that key is not in the set. When we delete or add there's no lookup cost either so we have constant time deletes, adds, and lookups. Not a perfect structure though.

First of all, this isn't useful for something an order with (a list of some sort) because your addresses won't have any notion of order.

Secondly, you need a sufficiently large footprint of memory to be able to store all of your objects without collisions. This can balloon quickly. 

Thirdly, you'll need a good hashing algorithm that spits out a viable address for table. That algorithms needs to have several qualities to it. It needs to be idempotent. Idempotent is a fancy way of saying that a function given an input always outputs the same output. function double(x) { return 2x; } would be an idempotent function because if I do double(5) a million times, on the million-and-first try I'll still get the answer 10. The function double is idempotent. Take the following function: 

 ```
var multiplier = 0;
function doublePlus(x) {
    multiplier++;
    return 2 * x * multiplier;
}
 ```
 
The above function is not idempotent because if I call I keep calling the doublePlus function with 5, I'm going to keep getting different answers. It is not idempotent because the function has side effects. Side effects are when calling a function makes some effect to the state surrounding it. You generally want to avoid side effects in programming as much as possible because it makes debugging much hard, makes your code less testable because it means you code must be in a certain state to work a certain way, and makes the code harder to read because you have to think about functions over term instead of in a vacuum because they depend on the code around them. Idempotence is critical in a good hashing function because given a certain input it always has to address the same place in memory or else the whole idea of a hash table falls apart. 

A good hashing algorithm needs to have a pretty good distribution of values. If it doesn't have a good distribution of values you are going to end up with collisions. Collisions happen when two inputs end up with the same the output, which means they are going to end up in the same spot in memory. That's a problem. An example of a poor hashing algorithm would be substituting 1 for a, 2 for b, 3 for c, etc. for a string. 'az' (1 + 26) and 'by' (2 + 25) are going to collide, as would 'za'. You need them to have a wide and as-even-as-possible distribution.

A good hashing algorithm needs to be performant too; the point of a hash table to have lightning fast lookups and writes; if your hashing algorithm is mega slow then you're defeating the purpose; ie don't use cryptographically secure algorithms!

The modulo operator (%) is important to understand in hashing too. Generally the numbers your hashing algorithms will generate huge numbers, numbers far larger than the size of your array. To ensure that your number falls in a legal limit of 0 to the largest index in the array, we're going to use the modulo operator. Remember doing long division in school? Where 10 / 3 = 3 remainder 1? The modulo operator give you just the remainder. So 10 % 3 = 1. It just totally throws away the result of the integer division. This is useful because now we can get huge numbers but still ensure they fall in an acceptable range. 
```
class HashTableSet {
  constructor() {
    this.table = new Array(255);
  }
  add(input) {
    this.table[this.hash(input, 255)] = input;
  }
  check(input) {
    return !!this.table[this.hash(input, 255)];
  }
  hash(input, max) {
    let num = 0;
    for (let i = 0; i < input.length; i++) {
      num += input.charCodeAt(i) * i;
    }
    return num % max;    
  }
}
 ```
## Functional Programming
Learning to functional program, whether you choose to adhere to its tenants going forward or not, will make you a much better programmer. It teaches you ways to structure your code to make it maintainable, compose able, and easy to reason about. 

Key concepts, first, would be avoiding side effects. We want to minimize where we affect state. This makes our program easier to reason about because we can easily reason through individual parts of our code. If your code has a lot of state that gets modified everywhere then you have reason through your code over time instead of being able to take tiny snapshots of individual functions. A function that modifies no state and is idempotent is called a pure function. We generally want small, focused, pure functions. 

Second, higher order function. Because JavaScript has functions as first-class citizens, this makes pattern possible. We can pass functions into other functions, and this pattern of composition makes for some powerful paradigms. Pure functions are important parts of higher order functions because we're going to run this functions over and over again. 

Third, transforming lists of data. When you're operation exclusively on lists, it's called vector or array programming. When you're doing that, you can depend on the fact that you can take the output of one function and safely put that into the next function. We can chain calls together. Our code becomes expressive at this point. We begin describe what we want to happen rather than imperatively telling how. 

### Map
Map is a higher order function. That is to say it takes in another function and has its own logic on how to apply that function.

Map has similarities to forEach. It takes a function in and applies that function individually to each element in that array. Where it differs from forEach is that map creates a new array of the values returned within the function. It allows you to transform whole lists of values without modifying the original list. 
```
const double = num => 2*num;
const doubleEach = input => input.map( double );

const square = num => num*num;
const squareEach = input => input.map( square );

const doubleAndSquareEach = input => input.map(double).map(square);

const myMap = (array, fn) => {
  const answer = [];
  for (let i = 0; i < array.length; i++) {
    answer.push(fn(array[i]));
  }
  return answer;
};
```

### Reduce
Reduce is really useful when you a have a list of values that you want to combine in some meaningful way down to one value. You'll often hear the term map/reduce thrown around in regards to data science; they're used a lot in that sense because you're taking large sets of data, doing some transformations on them to get them in a certain state, and then reducing them down to useful statistics.

A reduce function involves a list it's being called, a function that does the reducing, the accumulator, and the seed value. The accumulator is the interim value that is passed into each call of the reducer function that the function then returns. The value returned is then passed into the next call of the reducer function on the next value. The seed value is the value of the first accumulator. If there's no seed value, the zero index in the array is the seed. 
```
var list = ['a','b','c'];
list.reduce(function(accumulator, letter) {
    return accumulator + letter.toUpperCase();
}); // returns aBC since a becomes the seed

list.reduce(function(accumulator, letter) {
    return accumulator + letter.toUpperCase();
}, ''); // returns ABC since '' starts as the seed
```

```
const addTogether = list => {
  return list.reduce((acc, num) => acc+num, 0);
};

const concatenateStringsWithSpaces = list => {
  return list.reduce((acc, string) => acc + string + " ", "");
};

const squaresAndSubtracts = list => {
  return list
    .map( num => num*num )
    .reduce( (accumulator, num) => accumulator-num );
};

const myReduce = (list, fn, seed) => {
  let answer = seed;
  for (let i = 0; i < list.length; i++) {
    answer = fn(answer, list[i]);
  }
  return answer;
};
```

### Filter
Filter does exactly what it sounds like: it takes a list of items and pares out some of the items you don't need in the list. All you have to do is write a filter function that returns true if you want the item to stay in the list or false if you want it removed from the list. The returned result is a new list with just the items you returned true on. 
```
const filterOutOdds = nums => nums.filter( num => num % 2 === 0);

const filterState = (list, state) => list.filter( person => person.state === state );

const showOutOfCADevs = list => {
  return list
    .filter( person => person.state !== 'CA')
    .map( person => person.name.toUpperCase() )
    .reduce( (acc, name) => `${acc}, ${name}` );
};

const myFilter = (list, fn) => {
  const answer = [];
  for (let i = 0; i < list.length; i++) {
    if (fn(list[i])) {
      answer.push(list[i]);
    }
  }
  return answer;
};
```


## Bloom Filters
Bloom filters are an interesting data structure which are designed to tell you quickly and efficiently if an item is in a set. In exchange for being really fast and memory efficient, bloom filters trade off the fact that it can't tell you definitely if an item is in the set; it can only tell you definitely that item is not in the set. Stated differently, bloom filters have a false positive rate but do not have false negatives.

Sometimes you don't care about false positives, you just want to make sure something is not in the set. What about that false positive rate? Well, they'll just filter out something they could have shown you and then show you something they definitely can show you. It's an acceptable trade off.

Imagine you have an array with ten elements in it. Every element in the array is a 0 bit. This is an empty bloom filter. Now we want to add "George" to the array.

Okay, so I run my string through three different hashing functions and they give me 2, 5, and 8. I'll flip all those bits at those indexes so my new array is [0, 0, 1, 0, 0, 1, 0, 0, 1, 0].

After doing this, I'll check to see if "Sarah" is in the array. After running through the hashing function, they give 2, 2, and 4. 2 is flipped but 4 is not, so I can definitively say that "Sarah" is not in the data set.

So let's add one more item to the array, "Simona". The indexes we get back 0, 4, and 5. So now our array is [1, 0, 1, 0, 1, 1, 0, 0, 1, 0]. We flip both 0 and 4 indexes and 5 was already flipped so we do nothing to it. Now what happens if we check "Sarah" again? This time we'll get a false positive that "Sarah" is in the dataset. That's why the two answers you can get back from the question "Is X in the bloom filter" are no and maybe.

So when you add more items to a bloom filter, you'll increase your false positive rate. You can mitigate this by having a larger array, but you'll be trading off on having a larger memory footprint. You can also have more or less hashing functions, trading off on how quickly memory will fill up versus false positive rates.
```
// Hashing functions. it's not essential to know how they work
// a library called xxhashjs is being loaded (as XXH) and we're using three different
// instances of that as your hashing functions
const h1 = string => Math.abs(XXH.h32(0xABCD).update(string).digest().toNumber() % 100);
const h2 = string => Math.abs(XXH.h32(0x1234).update(string).digest().toNumber() % 100);
const h3 = string => Math.abs(XXH.h32(0x6789).update(string).digest().toNumber() % 100);

// fill out these two methods
// `add` adds a string to the bloom filter and returns void (nothing, undefined)
// `check` takes a string and tells you if a string is maybe in the bloom filter
class BloomFilter {
  _array = new Array(100).fill(0);
  add(string) {
    this._array[h1(string)] = 1;
    this._array[h2(string)] = 1;
    this._array[h3(string)] = 1;
  }
  contains(string) {
    return !!(this._array[h1(string)] && this._array[h2(string)] && this._array[h3(string)]);
  }
};
```
## Tree Traversals
Trees are an essential part of storing data, or at computer scientists like to refer them as, data structures. Among their benefits is that they're optimized to be searchable. Occasionally you need to serialize the entire tree into a flat data structure. 


### Depth-first Traversal
One variant depth-first traversals: pre-order traversal. The basic gist is that for each of the nodes, you process the node (in our case, save it to an array since we're serializing this tree,) then process the left subtree and then the right tree.

We end up with the array of [8, 3, 1, 6, 4, 7, 10, 14, 13]. This is called preorder traversal.

The other variants are quite similar; the only thing we do is change the order. "process the node," mean you do whatever operation you're going to do: add it to an array, copy the node, or whatever that may be.

In preorder traversal, you process the node, then recursively call the method on the left subtree and then the right subtree.

In inorder traversal, you first recursively call the method on the left tree, then process the node, and then call the method on the right tree.

Postorder traversal, as you have guessed, you recursively call the method on the left subtree, then the left subtree, then you process the node. The results of these are as follows:
```
// preorder
[8, 3, 1, 6, 4, 7, 10, 14, 13]

// inorder
[1, 3, 5, 6, 7, 8, 10, 13, 14]

// postorder
[1, 4, 7, 6, 3, 13, 14, 10, 8]
```

For a sorted list out of a BST, you'd want to use inorder. If you're making a deep copy of a tree, preorder traversal is super useful since you'd copy a node, and then add its left child and then its right tree. Postorder would be useful if you're deleting a tree since you'd process the left tree, then the right, and only after the children had been deleted would you delete the node you're working on.
```
const preorderTraverse = (node, array) => {
  if (!node) return array;
  array.push(node.value);
  array = preorderTraverse(node.left, array);
  array = preorderTraverse(node.right, array);
  return array;
};

const inorderTraverse = (node, array) => {
  if (!node) return array;
  array = inorderTraverse(node.left, array);
  array.push(node.value);
  array = inorderTraverse(node.right, array);
  return array;
};

const postorderTraverse = (node, array) => {
  if (!node) return array;
  array = postorderTraverse(node.left, array);
  array = postorderTraverse(node.right, array);
  array.push(node.value);
  return array;
};
```

### Breadth-first Traversal
Now that you've done depth-first, let's tackle breadth-first. Breadth-first isn't recursive processing of subtrees like depth-first. Instead we want to process one layer at a time. Using the tree above, we want the resulting order to [8, 3, 10, 1, 6, 14, 4, 7, 13]. In other words, we start at the root, and slowly make our way "down" the tree.

The way we accomplish this is using the queue. 

What we're going to do is process the node, then add the left child to the queue and then add the right child to the queue. After that, we'll just dequeue an item off of the queue and call our function recursively on that node. You keep going until there's no items left in the queue.
```
// recursive
const breadthFirstTraverse = (queue, array) => {
  if (!queue.length) return array;
  const node = queue.shift();
  array.push(node.value);
  if (node.left) queue.push(node.left);
  if (node.right) queue.push(node.right);
  return breadthFirstTraverse(queue, array);
}

// iterative
const breadthFirstTraverse2 = (queue, array) => {
  if (!queue.length) return array;
  
  while (queue.length) {
    const node = queue.shift();
    array.push(node.value);
    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }
  
  return array;
}
```
Breadth-first traversals are useful for many things, the gist of when you use them is that you know the answer for what you're looking for is "closer" to the root node as opposed to far away when you would use depth-first. Again, it's all trade-offs.

## Graphs
Graphs are all about modeling relations between many items. For example, think of Facebook's Social Graph. I'm friends with you and you're friends with me. But you're also friends with six hundred other people which is about five hundred fifty too many. Those people in turn also have too friends. But many of my friends are your friends, so the connections aren't linear, they're … well, they're graph-like.

In the Facebook example, each person would be a node. A node represents some entity, much like a row in an SQL database. Every so-called "friendship" would be called an edge. An edge represents some connection between two items. In this case, our Facebook friendship is bidirectional: if I'm friends with you then you're friends with me. Twitter would be an example of a unidirectional edge: just because I follow you doesn't mean you follow me.

Graphs are everywhere. Your various social networks, your Internet of Things devices that have relationships with each other, your neural-networks machine-learning libraries, everywhere. As we continue to model more-and-more of the natural world in virtual space graphs become ever-more important since relationships between things and beings exist all around us.

```
// you work for a professional social network. in this social network, a professional
// can follow other people to see their updates (think Twitter for professionals.)
// write a function that finds the job `title` that shows up most frequently given
// a set of degree of separation from you. count the initial id's own job title in the total

/*
  parameters:
  myId                - number    - the id of the user who is the root node
  getUser             - function - a function that returns a user's object given an ID
  degreesOfSeparation - number   - how many degrees of separation away to look on the graph
*/

const findMostCommonTitle = (myId, getUser, degreesOfSeparation) => {
  let queue = [myId];
  const seen = new Set();
  const jobs = {};
  
  for (let i = 0; i <= degreesOfSeparation; i++) {
    queue = queue
      .filter((id) => !seen.has(id))
      .map(getUser)
      .map(user => {
        jobs[user.title] = jobs[user.title] ? jobs[user.title] + 1 : 1;
        seen.add(user.id)
        return user;
      })
      .map((user) => user.connections)
      .reduce((acc, users) => acc.concat(users), [])
  }
  return Object.keys(jobs)
    .map((job) => [job, jobs[job]])
    .sort((a, b) => {
      if (a[1] > b[1]) return -1;
      if (a[1] < b[1]) return 1;
      return 0;
    })[0][0]
}
```
## Tries
The word "trie" is a play on the fact that this particular data structure makes it easy to retrieve data, so trie is said just like it is there, tree. However, because tries and trees are often discussed together, you'll here people call them "tries" (as in the plural try) or try to disambiguate them in other methods. 

It's a tree that's optimized for searching by prefix. The classic example of what you would use this for is autocomplete: you know when you type in "San" and it offers suggestions of what to finish with like "Francisco", "Diego", or "Jose". Tries are really useful for that.

A trie starts with a root node that doesn't represent anything (often it's given the value of '' (empty string.) It has a bunch of child nodes (as many are necessary) that represent one letter, the first letter of all the words added to the data structure. Each of those letter-nodes will have children nodes for all the second letters of the words that are represented in the data structure. So on and so forth, there will be a chain of nodes that represent each letter in the data structure.

If a user types bo in the text input, you can go through your data structure, find the o node in that chain, and then all you have to do is a depth-first traversal of the children nodes to for a list of autocomplete suggestions.
```
  a – [various children]
 /
b – o – s – t – o – n
     \
      i – s – e
```
So based on this, you'd get suggestions of "Boston" and "Boise".

Since some words are contained within chains of others (for example, there are two separate cities, one called "Salina" and one called "Salinas" or "Sandy" and "Sandy Springs".) You'll often have a flag in there that signifies the node you're on is a complete word so you can just add it to the list and then keep going on the children.

There are more complicated things you can do with tries as well that we won't explore here. You can have autocompletes for mid-word completions (if I type "francisco" it won't autocomplete "san francisco" at the moment.) You can add weights to certain edges/children so they're suggested first (so San Francisco comes before San Mateo.) But this exercise, assume all words weighted equally.

You'll also represent a space in the tree as its own node so when you type san<space> it autocompletes San Francisco instead of Santa Fe. In other words, no characters are given special treatment. That can be unintuitve.
```
 class Node {
  children = [];
  value = "";
  terminus = false;
  constructor(string) {
    this.value = string[0] || "";
    if (string.length > 1) {
      this.children.push(new Node(string.substr(1)));
    } else {
      this.terminus = true;
    }
  }
  add(string) {
    const value = string[0];
    const next = string.substr(1);
    for (let i = 0; i < this.children.length; i++) {
      const child = this.children[i];
      if (child.value === value) {
        if (next) {
          child.add(next);
        } else {
          child.terminus = true;
        }
        return;
      }
    }

    this.children.push(new Node(string));
  }
  _complete(search, built, suggestions) {
    if (suggestions.length >= 3 || (search && search[0] !== this.value)) {
      return suggestions;
    }

    if (this.terminus) {
      suggestions.push(`${built}${this.value}`);
    }

    this.children.forEach(child =>
      child._complete(search.substr(1), `${built}${this.value}`, suggestions)
    );

    return suggestions;
  }

  complete(string) {
    return this.children
      .map(child => child._complete(string, "", []))
      .reduce((acc, item) => acc.concat(item));
  }
}

const createTrie = words => {
  const root = new Node("");
  words.forEach(word => root.add(word.toLowerCase()));
  return root;
};
```

## Searching for an Element in an Array
This very similar to sorting, as you'll quickly figure out. Search is the act of looking for a particular element in an array.

There are essentially two common ways of doing search: linear search and binary search. The former is the simplest code and really only useful if the list you're searching on is not sorted in any way. You just go through from 0 to the length of the array and ask "is the is the element I'm looking for?" No frills here. Its complexity is O(n).

Binary search is a bit more interesting. It only works if the array is already sorted. To explain it, let's take the example of how you find a name in a telephone book (if you even know what that is anymore!) A telephone book is a sorted list of names. You'll open the book more or less to the middle (or say you do, for argument's sake.) From there, if the name you're looking for is smaller/earlier in the alphabet, you'll go halfway to the smaller/earlier side of the book, and so-on-and-so-forth, keeping going halfway until eventually you land on the name you're looking for. Let's see how that works in practice.
```
0, 5, 10, 12, 15, 19, 21, 22, 24, 30]

search for 12

start in the middle, is 19 === 12? no, smaller, go left

look in the middle of the smaller half, 10 === 12? no, larger, go right

look in the middle of the larger half (which is now just one number), is 12 === 12? yes, found element
```

This turns out to work quickly even on extremely large datasets. Its complexity is O(log n).

```
function linearSearch(id, array) {
  for (let i = 0; i < array.length; i++) {
    if (id === array[i].id) {
      return array[i];
    }
  }
  return void 0;
}

function binarySearch(id, array) {
  let min = 0;
  let max = array.length - 1;
  let index;
  let element;

  while (min <= max) {
    index = Math.floor((min + max) / 2);
    element = array[index];

    if (element.id < id) {
      min = index + 1;
    } else if (element.id > id) {
      max = index - 1;
    } else {
      return element;
    }
  }

  return void 0;
}
```

## Heap Sort
A heap is an array that represents a tree data structure and has to be sorted in a particular way to represent that tree. Priority queues are often represented as heaps and often those two terms are used interchangeably even if the the priority queue is implemented a different way.

Once you construct a heap, removing an item from it is done in constant time since you need to find the next largest node to move to the root. This process is typically called heapify. In order to construct a max heap, you run heapify starting at the middle of the array and work backwards to the root. You don't need to do it from the end because heapify will inherently look at those nodes.

So the process of heapsort is:
* Make the array a max heap
* Loop over the array, dequeuing the root node (which will give you the largest item) and swapping that with last item in the array
* After dequeuing each item, run heapify again (same function we used to create the heap) once to find the next root node
* Next loop you'll dequeue the root node and swap it with the second-to-last item in the array and run heapify again.
* Once you've run out of items to dequeue, you have a sorted array! Let's see what that looks like.

```
// initial array
[5, 3, 2, 10, 1, 9, 8, 6, 4, 7]

// heapify the array
start at index 5, value 9
its left child is at index 11 and right 12, out of bounds
nothing to do, next iteration

i-- index 4, value 1
left child is index 9 value 7, right child is index 10, out of bounds
7 is larger than 1, swap left child and parent
[5, 3, 2, 10, 7, 9, 8, 6, 4, 1]
call heapify on index 9, does nothing

i-- index 3, value 10
left child is index 7 value 6, right child is index 8 value 4
neither is larger than 10
nothing to do, next iteration

i-- index 2, value 2
left child is index 5 value 9, right child is index 6 value 8
9 is the largest number, swap with parent
[5, 3, 9, 10, 7, 2, 8, 6, 4, 1]
call heapify on index 5, does nothing

i-- index 1, value 3
left child is index 3 value 10, right child is index 4 value 7
10 is in the largest number, swap with parent
[5, 10, 9, 3, 7, 2, 8, 6, 4, 1]
call heapify on index 3
left child is index 7 value 6, right child is index 8 value 4
6 is larger, swap with parent
[5, 10, 9, 6, 7, 2, 8, 3, 4, 1]
call heapify on index 7, does nothing

i-- index 0, value 5
left child is index 1 value 10, right child is index 2 value 9
10 is in the largest number, swap with parent
[10, 5, 9, 6, 7, 2, 8, 3, 4, 1]
call heapify on index 1
left child is index 3 value 6, right child is index 4 value 7
7 is larger, swap with parent
[10, 7, 9, 6, 5, 2, 8, 3, 4, 1]
call heapify on index 4
left child is index 9 value 1, right child is index 10, out of bounds
parent is larger, does nothing
```

Now our array is officially a heap. Now we can begin dequeuing items and sorting our array.

```
Swap 10 and 1
[1, 7, 9, 6, 5, 2, 8, 3, 4, 10]
call heapify on index 0
left child is index 1 value 7, right child is index 2 value 9
9 is the larger, swap with parent
[9, 7, 1, 6, 5, 2, 8, 3, 4, 10]
call heapify on index 2
left child is index 5 value 2, right child is index 6 value 8
8 is larger, swap with parent
[9, 7, 8, 6, 5, 2, 1, 3, 4, 10]
call heapifiy on index 6, does nothing since children are out of bounds

Swap 9 and 4
[4, 7, 8, 6, 5, 2, 1, 3, 9, 10]
call heapify on index 0

Continue swapping the first element (the root) and last element of the heap
and then call heapify on element 0
After all these iterations, the array will be sorted
```

Example:
```
const heapSort = (array) => {
  snapshot(array);
  array = createMaxHeap(array);
  let heapSize = array.length;
  let temp;
  for (let i = array.length - 1; i > 0; i--) {
    temp = array[0];
    array[0] = array[i];
    array[i] = temp;
    heapSize--;
    heapify(array, 0, heapSize);
  }
  snapshot(array);
  return array;
}

const createMaxHeap = (array) => {
  for (let i = Math.floor(array.length / 2); i >= 0; i--) {
    heapify(array, i, array.length);
  }
  return array;
}

const heapify = (array, index, heapSize) => {
  const left = 2 * index + 1;
  const right = 2 * index + 2;
  
  let largestValueIndex = index;
  
  if (heapSize > left && array[largestValueIndex] < array[left]) {
    largestValueIndex = left;
  }
  
  if (heapSize > right && array[largestValueIndex] < array[right]) {
    largestValueIndex = right;
  }
  
  if (largestValueIndex !== index) {
    const temp = array[index];
    array[index] = array[largestValueIndex];
    array[largestValueIndex] = temp;
    heapify(array, largestValueIndex, heapSize);
    snapshot(array);
  }
}
```

## Radix Sort
Radix sorting is non-comparison based sorting. Up to this point all of the sorts have been comparison based sorts. That is to say, we decide the order of the numbers based on asking the question is this element bigger than that one over-and-over again until numbers are in order and the rest of the algorithm is just optimizing how often we ask that question. The big O of these comparison based algorithms cannot be any faster n log n so in order to get beyond that, we have to change what we're doing. We have to sort based on other criteria.

Enter non-comparison based algorithms. There are a few variations but radix sort is one of the more useful algorithms. The basic idea is we're to enqueue each number in different queues based on what the last digit in the digit of the number (the "ones" place.) Once we do that, we'll dequeue each queue in order back into the original array. If you think about it, it'll everything will be sorted up to the the ones place. So your array will look like [10, 1, 52, 102, 33, 45, 6, 18, 9] or something like that. Notice all the ones places are in ascending order; just nothing else is. After we've done this, we'll repeate the process again but with the tens place. With the former example, it'd look like [1, 102, 6, 9, 10, 18, 33, 45, 52]. Lastly we'll do the process on the hundreds place (which in this example is just going to be the 0 bucket and the 1 bucket) and end up with [1, 6, 9, 10, 18, 33, 45, 52, 102]. That's it! It's sorted.

```
function getDigit (number, place, longestNumber) {
  const string = number.toString();
  const size = string.length;
  
  const mod = longestNumber - size;
  return string[place - mod] || 0;
}

function findLongestNumber(array) {
  let longest = 0;
  for (let i = 0; i < array.length; i++) {
    const currentLength = array[i].toString().length;
    longest = currentLength > longest ? currentLength : longest;
  }
  return longest;
}

function radixSort(array) {
  snapshot(array);
  const longestNumber = findLongestNumber(array);
  
  const buckets = new Array(10).fill().map(() => []); // make an array of 10 arrays
  
  for (let i = longestNumber - 1; i >= 0; i--) {
    while (array.length) {
      const current = array.shift();
      buckets[getDigit(current, i, longestNumber)].push(current);
    }
    
    for (let j = 0; j < 10; j++) {
      while (buckets[j].length) {
        array.push(buckets[j].shift());
      }
    }
    snapshot(array);
  }
  
  return array;
}
```
