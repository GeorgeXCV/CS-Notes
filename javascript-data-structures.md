# Data Structures
Collection of values, the relationships among them, and the functions or operations that can be applied to the data.

## Singly Linked Lists
Linked Lists contains nodes, each node has a value and a pointer to another node or null.

Head = start of list
Tail = end of list
Length = length of list

Do not have indexes.

Random access is not allowed.

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
  
  push(val) {
      var newNode = new Node(val);
      if (!this.head) {
          this.head = newNode;
          this.tail = this.head;
      } else {
        this.tail.next = newNode;
        this.tail = newNode;
      }
      this.length++;
      return this;
  }
  
  pop() {
    if (!this.head) return undefined;
    var current = this.head;
    var newTail = current;
    while (current.next) {
      newTail = current;
      current = current.next;
    }
    this.tail = newTail;
    this.tailnext = null;
    this.length--;
    if (this.length === 0) {
      this.head = null;
      this.tail = nulll
    }
    return current;
  }
  
  shift() {
    if (!this.head) return undefined;
    var currentHead = this.head;
    this.head = currentHead.next;
    this.length--;
    return currentHead;
  }
  
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
}

var list = new SinglyLinkedList();
list.push("Hi);
```
