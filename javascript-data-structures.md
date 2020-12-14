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
