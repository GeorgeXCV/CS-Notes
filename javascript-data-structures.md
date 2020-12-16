# Data Structures
Collection of values, the relationships among them, and the functions or operations that can be applied to the data.

## Singly Linked Lists
Linked Lists contains nodes, each node has a value and a pointer to another node or null.

Head = start of list
Tail = end of list
Length = length of list

Do not have indexes.

Random access is not allowed.

Better than arrays when insertion and deletion at the beginning are frequently required.

```
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
      this.head = null;
      this.tail = null;
      this.length = 0;
  }
  
  // Add new value to end
  push(val) {
      var newNode = new Node(val);
      // If no items in list, set value as the head
      if (!this.head) {
          this.head = newNode;
          this.tail = this.head;
      } else {
        // Add the new value to the end
        this.tail.next = newNode;
        this.tail = newNode;
      }
      this.length++;
      return this;
  }
  
  // Remove last value
  pop() {
    if (!this.head) return undefined;
    var current = this.head;
    var newTail = current;
    // Loop to end of list
    while (current.next) {
      newTail = current;
      current = current.next;
    }
    this.tail = newTail; // Pointer before last
    this.tail.next = null; // Remove last item
    this.length--;
    if (this.length === 0) {
      this.head = null;
      this.tail = nulll
    }
    return current;
  }
  
  // Remove first element
  shift() {
    if (!this.head) return undefined;
    var currentHead = this.head;
    this.head = currentHead.next;
    this.length--;
    return currentHead;
  }
  
  // Add new value to start
  unshift(val) {
    var newNode = new Node(val);
    if (!head) {
        this.head = newNode;
        this.tail = this.head
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }
  
  // Get index
  get(index) {
      if (index < 0 || index >= this.length) return null;
      var counter = 0;
      var current = this.head;
      while (counter !== index) {
          current = current.next;
          counter++;
      }
      return current;
  }
  
  // Set index to new value
  set (index, val) {
      var foundNode = this.get(index);
      if (foundNode) {
            foundNode.val = val;
            return true;
      }
      return false;
  }
  
  // Insert index
  insert (index, val) {
      if (index < 0 || index > this.length) {
            return false;
      }
      // If index at end, push value to end
      if (index === this.length) {
          !!return this.push(val);
      }
      // If index at start, add value before first item
      if (index === 0) {
          !!this.unshift(val);
      }
     
      var newNode = new Node(val);
      // Get node before index we want to insert at
      var prev = this.get(index -1);
      // Make a copy of item ahead
      var temp = prev.next;
      // Set next pointer to equal our new node
      prev.next = newNode;
      // Set next pointer of new node to equal value that was previously here
      newNode.next = temp;
      this.length++;
      return true;
  }
  
  // Remove item via index
  remove(index) {
      if (index < 0 || index >= this.length) return undefined;
      if (index === 0) return this.shift();
      if (index === this.length -1) return this.pop();
      var previousNode = this.get(index -1);
      var removed = previousNode.next;
      previousNode.next = removed.next;
      this.length--;
      return removed;
  }
  
  // Reverse the list
  reverse() {
      var node = this.head;
      this.head = this.tail;
      this.tail = node;
      var next;
      var prev = null;
      for (var i = 0; i < this.length; i++) {
          next = node.next;
          node.next = prev;
          prev = node;
          node = next;
      }
      return this;
  }
  
}

var list = new SinglyLinkedList();
list.push("Hi);
```
## Doubly Linked List
Identical to Singly Linked List except every node has another pointer, to the previous node.

Better than Singly Linked Lists for finding nodes, can be done in half the time.

Take ups more memory than Singly Linked List but has more flexability. 

```
class Node{
    constructor(val){
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList{
    constructor(){
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    
  push(val){
        var newNode = new Node(val);
        if(this.length === 0){
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }
    
     pop(){
        if(!this.head) return undefined;
        var poppedNode = this.tail;
        if(this.length === 1){
            this.head = null;
            this.tail = null;
        } else {
            this.tail = poppedNode.prev;
            this.tail.next = null;
            poppedNode.prev = null;
        }
        this.length--;
        return poppedNode;
    }
    
    // Remove first element
    shift () {
        if (this.length === 0) return undefined;
        var oldHead = this.head;
        if (this.length === 1) {
            this.head = null;
            this.tail = null;
        } else {
          this.head = oldHead.next;
          this.head.prev = null;
          oldHead.next = null;
        }
        this.length--;
        return oldHead;   
    }
    
    // Add node to the beginning 
    unshift(val) {
        var newNode = new Node(val);
        if (this.length === 0) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.head.prev = newNode;
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
    
    // Accessing a node by its position
    get(index) {
        if (index < 0 || index >= this.length) return null;
        var count, current;
        if (index <= this.length / 2) {
            count = 0;
            current = this.head;
            while (count !== index) {
                  current = current.next;
                  count++;
            }
        } else {
            count = this.length -1;
            current = this.tail;
            while (count !== index) {
                current = current.prev;
                count--;
            }
        }  
       return current;
    }
    
    // Replacing the value of a node
    set (index, val) {
      var foundNode = this.get(index);
      if (foundNode) {
            foundNode.val = val;
            return true;
      }
      return false;
    }
    
    // Add a node at a certain position
    insert() {
        if (index < 0 || index > this.length) return false;
        if (index === 0) return !!this.unshift(val);
        if (index === this.length) return !!this.push(val);
        
        var newNode = new Node(val);
        var beforeNode = this.get(index-1);
        var afterNode = beforeNode.next;
        
        beforeNode.next = newNode;
        newNode.prev = beforeNode;
        newNode.next = afterNode;
        afterNode.prev = newNode;
        this.length++;
        return true;
    }
    
    // Remove a node at a certain position
    remove (index) [
        if (index < 0 || index >= this.length) return undefined;
        if (index === 0) return this.shift();
        if (index === this.length -1) return this.pop();
        
        var removedNode = this.get(index);
        var beforeNode = removedNode.prev;
        var afterNode = removedNode.next;
        beforeNode.next = afterNode;
        afterNode.prev = beforeNode;
        removedNode.next = null;
        removedNode.prev = null;
        this.length--;
        return removedNode;
        
    }
    
}
```

## Stacks
The last element added to a stack is going to be the first one to be removed.

Used for managing function invocations (the call stack), and undo/redo.

They are not a built in data structure in JavaScript.

## Queue
First In First Out, just like an actual queue. 

## Trees
Trees are non-linear data structures that contain root and child nodes.

Binary Trees can have values of any type, but at most two children for each parent. Are used to compare values.

Binary Search Trees are a more specific version of Binary Tres where ever node to the left of a parent node is always less than the parent and every node to the right of a parent node is always greater than the parent.

```
class Node {
    constructor(value) {
        this.value = valuie;
        this.left = null;
        this.right = null;
    }
}

class BinarySearchTree {
      constructor() {
          this.root = null;
      }
      
      insert(value) {
          var newNode = new Node(value);
          if (this.root === null) {
              this.root = newNode;
              return this;
          } else {
              var current = this.root;
              while (true) {
                 if (value === curent.value) return undefined;
                 if (value < current.value) {
                      if (current.left === null) {
                          current.left = newNode;
                          return this;
                      } else {
                          current = current.left;
                      }
                 } else if (value > current.value) {
                        if (current.right === null) {
                            current.right = newNode;
                            return this;
                        } else {
                            current = current.right;
                        }
                   }
              }
          }
      }
      
      find (value) {
          if (this.root === null) return false;
          var current = this.root;
          var found = false;
          while (current && !found) {
                if (value < current.value) {
                    current = current.left;
                } else if (value > current.value) {
                    current = current.right;
                } else {
                    return true;
                }
          }
          return false;
      }
}
```

## Breadth First Search
Search each element left to right, don't drop level until all checked above.

```
  breadthFirstSearch() {
      var data = [];
      var queue = [];
      var node = this.root;
      queue.push(node);
      while (queue.length) {
            node = queue.shift()
            data.push(node.value);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
      }
      return data;
  }
```

## Depth First Search
Traverse all nodes downwards until moving to the right.

```
  depthFirstSearchPreOrder() {
       var data = [];
       function traverse(node) {
          data.push(node.value);
          if(node.left) traverse(node.left);
          if(node.right) traverse(node.right);
       }
       traverse(this.root);
       return data;
  }
```

## Depth First Post Order
Root is the last thing thats visited.

For any node, we visit all children before the node, still left to right.

```
  depthFirstSearchPostOrder() {
      var data =[];
      function traverse(node) {
          if(node.left) traverse(node.left);
          if(node.right) traverse (node.right);
          data.push(node.value);  
       }
       traverse(this.root);
       return data;
      }
  }
```

## Depth First Search - In Order
Entire left side starting from bottom, then to root, then to right.

```
depthFirstSearchInOrder() {
      var data =[];
      function traverse(node) {
          if(node.left) traverse(node.left);
          data.push(node.value);  
          if(node.right) traverse (node.right);
       }
       traverse(this.root);
       return data;
      }
  }
```

## Heaps
Binary Heaps are used to implement Priority Queues which are very commonly used data structures. Also used commonly with graph traversal algorithms.

Max Binary Heap:
Each parent has at mode two child nodes.
The value of each parent node is always greater than its child nodes.

In a max Binary Heap the parent is greater than the children, but there are no gurantees between sibling nodes.

```
class MaxBinaryHeap {
    constructor() {
        this.values = [];
    }
    
    insert(element) {
        this.values.push(element);
        thius.bubbleUp();
    }
    
    bubbleUp() {
        let index = this.values.length -1;
        const element = this.values[index];
        while (index > 0) {
            let parentIndex = Math.floor((index -1)/2);
            let parent = this.values[parentIndex];
            if (element <= parent) break;
            this.values[parentIndex] = element;
            this.values[index] = parent;
            index = parentIndex;
        }
    }
    
    extractMax() {
        const max = this.values[0];
        const end = this.values.pop();
        if (this.values.length > 0) {
             this.values[0] = end;
             this.sinkDown();
        }
        return max;
    }
    
    sinkDown() {
        let index = 0;
        const length = this.values.length;
        const element = this.values[0];
        while (true) {
            let leftChildIndex = 2 * index + 1;
            let rightChildIndex = 2 * index + 2;
            let leftChild;
            let rightChild;
            let swap = null;
            
            if (letChildIndex < length) {
                leftChild = this.values[leftChildIndex];
                if (leftChild > element) {
                    swap = leftChildIndex;
                }
            }
            
            if (rightChildIndex < length) {
                rightChild = this.values[rightChildIndex];
                if ((swap === null && rightChild > element) || (swap !=== null && rightChild > leftChild)) {
                    swap = rightChildIndex;
                }
            }
            
            if (swap === null) break;
            this.values[index] = this.values[swap];
            this.values[swap] = element;
            index = swap;
            
        }
    }
}

```
## Priority Queue
A data structure where each element has a prioirty. Elements with higher priorities are served before elements with lower priorties.

Lower number denotes a higher priority.

```
lass PriorityQueue {
    constructor(){
        this.values = [];
    }
    enqueue(val, priority){
        let newNode = new Node(val, priority);
        this.values.push(newNode);
        this.bubbleUp();
    }
    bubbleUp(){
        let index = this.values.length - 1;
        const element = this.values[index];
        while(index > 0){
            let parentIndex = Math.floor((index - 1)/2);
            let parent = this.values[parentIndex];
            if(element.priority >= parent.priority) break;
            this.values[parentIndex] = element;
            this.values[index] = parent;
            index = parentIdx;
        }
    }
    dequeue(){
        const min = this.values[0];
        const end = this.values.pop();
        if(this.values.length > 0){
            this.values[0] = end;
            this.sinkDown();
        }
        return min;
    }
    sinkDown(){
        let index = 0;
        const length = this.values.length;
        const element = this.values[0];
        while(true){
            let leftChildIndex = 2 * index + 1;
            let rightChildIndex = 2 * index + 2;
            let leftChild,rightChild;
            let swap = null;

            if(leftChildIndex < length){
                leftChild = this.values[leftChildIndex];
                if(leftChild.priority < element.priority) {
                    swap = leftChildIdx;
                }
            }
            if(rightChildIndex < length){
                rightChild = this.values[rightChildIdx];
                if(
                    (swap === null && rightChild.priority < element.priority) || 
                    (swap !== null && rightChild.priority < leftChild.priority)
                ) {
                   swap = rightChildIndex;
                }
            }
            if(swap === null) break;
            this.values[index] = this.values[swap];
            this.values[swap] = element;
            index = swap;
        }
    }
}

class Node {
    constructor(val, priority){
        this.val = val;
        this.priority = priority;
    }
}
```

## Hash Tables
Used to store key-value pairs.

Like arrays but the keys are not ordered.

Each language has a version, JavaScript = Objects and Maps.

```
class HashTable {
  constructor(size=53){
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }
  set(key,value){
    let index = this._hash(key);
    if(!this.keyMap[index]){
      this.keyMap[index] = [];
    }
    this.keyMap[index].push([key, value]);
  }
  get(key){
    let index = this._hash(key);
    if(this.keyMap[index]){
      for(let i = 0; i < this.keyMap[index].length; i++){
        if(this.keyMap[index][i][0] === key) {
          return this.keyMap[index][i][1]
        }
      }
    }
    return undefined;
  }
  keys(){
    let keysArr = [];
    for(let i = 0; i < this.keyMap.length; i++){
      if(this.keyMap[i]){
        for(let j = 0; j < this.keyMap[i].length; j++){
          if(!keysArr.includes(this.keyMap[i][j][0])){
            keysArr.push(this.keyMap[i][j][0])
          }
        }
      }
    }
    return keysArr;
  }
  values(){
    let valuesArr = [];
    for(let i = 0; i < this.keyMap.length; i++){
      if(this.keyMap[i]){
        for(let j = 0; j < this.keyMap[i].length; j++){
          if(!valuesArr.includes(this.keyMap[i][j][1])){
            valuesArr.push(this.keyMap[i][j][1])
          }
        }
      }
    }
    return valuesArr;
  }
}
```

## Graphs

```
class Graph{
    constructor(){
        this.adjacencyList = {};
    }
    addVertex(vertex){
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
    addEdge(v1,v2){
        this.adjacencyList[v1].push(v2);
        this.adjacencyList[v2].push(v1);
    }
    removeEdge(vertex1,vertex2){
        this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(
            v => v !== vertex2
        );
        this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(
            v => v !== vertex1
        );
    }
    removeVertex(vertex){
        while(this.adjacencyList[vertex].length){
            const adjacentVertex = this.adjacencyList[vertex].pop();
            this.removeEdge(vertex, adjacentVertex);
        }
        delete this.adjacencyList[vertex]
    }
}
```

## Depth First Graph Traversal
Following the neighbours before backtracking, left to right.

```
depthFirstRecursive(start){
        const result = [];
        const visited = {};
        const adjacencyList = this.adjacencyList;

        (function dfs(vertex){
            if(!vertex) return null;
            visited[vertex] = true;
            result.push(vertex);
            adjacencyList[vertex].forEach(neighbor => {
                if(!visited[neighbor]){
                    return dfs(neighbor)
                }
            });
        })(start);

        return result;
    }
```

## Depth First Iterative
```
 depthFirstIterative(start){
        const stack = [start];
        const result = [];
        const visited = {};
        let currentVertex;

        visited[start] = true;
        while(stack.length){
            currentVertex = stack.pop();
            result.push(currentVertex);

            this.adjacencyList[currentVertex].forEach(neighbor => {
               if(!visited[neighbor]){
                   visited[neighbor] = true;
                   stack.push(neighbor)
               } 
            });
        }
        return result;
    }
```

## Breadth First
Vist neighbours at current depth first.

```
 breadthFirst(start){
        const queue = [start];
        const result = [];
        const visited = {};
        let currentVertex;
        visited[start] = true;

        while(queue.length){
            currentVertex = queue.shift();
            result.push(currentVertex);
           

            this.adjacencyList[currentVertex].forEach(neighbor => {
                if(!visited[neighbor]){
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            });
        }
        return result;
    }
```

## Dijkstra's Algorithm
Shortest path to node.

```
class WeightedGraph {
    constructor() {
        this.adjacencyList = {};
    }
    addVertex(vertex){
        if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
    }
    addEdge(vertex1,vertex2, weight){
        this.adjacencyList[vertex1].push({node:vertex2,weight});
        this.adjacencyList[vertex2].push({node:vertex1, weight});
    }
    Dijkstra(start, finish){
        const nodes = new PriorityQueue();
        const distances = {};
        const previous = {};
        let path = [] //to return at end
        let smallest;
        //build up initial state
        for(let vertex in this.adjacencyList){
            if(vertex === start){
                distances[vertex] = 0;
                nodes.enqueue(vertex, 0);
            } else {
                distances[vertex] = Infinity;
                nodes.enqueue(vertex, Infinity);
            }
            previous[vertex] = null;
        }
        // as long as there is something to visit
        while(nodes.values.length){
            smallest = nodes.dequeue().val;
            if(smallest === finish){
                //WE ARE DONE
                //BUILD UP PATH TO RETURN AT END
                while(previous[smallest]){
                    path.push(smallest);
                    smallest = previous[smallest];
                }
                break;
            } 
            if(smallest || distances[smallest] !== Infinity){
                for(let neighbor in this.adjacencyList[smallest]){
                    //find neighboring node
                    let nextNode = this.adjacencyList[smallest][neighbor];
                    //calculate new distance to neighboring node
                    let candidate = distances[smallest] + nextNode.weight;
                    let nextNeighbor = nextNode.node;
                    if(candidate < distances[nextNeighbor]){
                        //updating new smallest distance to neighbor
                        distances[nextNeighbor] = candidate;
                        //updating previous - How we got to neighbor
                        previous[nextNeighbor] = smallest;
                        //enqueue in priority queue with new priority
                        nodes.enqueue(nextNeighbor, candidate);
                    }
                }
            }
        }
        return path.concat(smallest).reverse();     
    }
}

class PriorityQueue {
    constructor(){
        this.values = [];
    }
    enqueue(val, priority){
        let newNode = new Node(val, priority);
        this.values.push(newNode);
        this.bubbleUp();
    }
    bubbleUp(){
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while(idx > 0){
            let parentIdx = Math.floor((idx - 1)/2);
            let parent = this.values[parentIdx];
            if(element.priority >= parent.priority) break;
            this.values[parentIdx] = element;
            this.values[idx] = parent;
            idx = parentIdx;
        }
    }
    dequeue(){
        const min = this.values[0];
        const end = this.values.pop();
        if(this.values.length > 0){
            this.values[0] = end;
            this.sinkDown();
        }
        return min;
    }
    sinkDown(){
        let idx = 0;
        const length = this.values.length;
        const element = this.values[0];
        while(true){
            let leftChildIdx = 2 * idx + 1;
            let rightChildIdx = 2 * idx + 2;
            let leftChild,rightChild;
            let swap = null;

            if(leftChildIdx < length){
                leftChild = this.values[leftChildIdx];
                if(leftChild.priority < element.priority) {
                    swap = leftChildIdx;
                }
            }
            if(rightChildIdx < length){
                rightChild = this.values[rightChildIdx];
                if(
                    (swap === null && rightChild.priority < element.priority) || 
                    (swap !== null && rightChild.priority < leftChild.priority)
                ) {
                   swap = rightChildIdx;
                }
            }
            if(swap === null) break;
            this.values[idx] = this.values[swap];
            this.values[swap] = element;
            idx = swap;
        }
    }
}

class Node {
    constructor(val, priority){
        this.val = val;
        this.priority = priority;
    }
}
```

## Dynamic Programming
Solving a problem by breaking it down into a collection of simplier subproblems, solving each of those subproblems once and storing their soultions.
