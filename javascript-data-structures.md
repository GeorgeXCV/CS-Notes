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
