## Linked Lists
- `Linked lists` are often compared to `arrays`
- `Arrays` have `indexes` but `linked lists don't`
- `Arrays` are in `contiguous places` in memory `linked list` aren't
- `Linked lists` have a variable called `head` that `points` to the `first item`
- `Linked lists` have another varibale called `tail` that points to the `last item`
- Each item in the `linked list` points to the `next` item, and the `last one` points to `null`

## Linked Lists Big O

### Adding and removing item from the end of a linked list
- For `adding a new node `, last item will point to the newly added item, and the pointer of tail will be set to the pointer of the last item
- There will be one execution or operation for this so the big O is `O(1)`
- `Popping` or removing an item from the end of a linked list is different
- In order to ensure `tail` point to the last item, we need to set the tail pointer to be equal to the pointer that is pointing to the last node
- Since we can't go back in the linked list, In order to get that pointer, we need to start from `head` and iterate though the list
- To get the pointer, and set tail equal to that pointer which points to the last item, we need to iterate through the list, so the big O is `O(n)`.

### Adding and removing item from the begining of a linked list
- If we wanna `add` an item to the `begining` of a linked list
- There must be a pointer that points to the begining of a linked list
- That pointer is the pointer of `head` which points to the first item in the linked list
- For this reason we set the pointer of newly added item to the pointer of the `head`
- Then set the `head` to point to the new node, the big O of this is `O(1)`
- For `removing` an item from the begining of a list
- Since we have an element which points to the 1st node(0 index)
- We set the `head` to `head.next` and then remove the first node, the big O is `O(1)`

### Adding and removing item from the middle of a linked list
- If we want to insert an item at the index of 3
- We need to start from `head` and iterate through the array to get to this point
- We want the new item to point to the same item that index 2 is pointing to
- Then we set the 2nd index to point to the newly added node
- Because we had to start at the head, and iterate through the list to be able to get to the point
- The time complexity is `O(n)`
- If we wanna remove the item at the index of 3
- We need to start from the head and iterate through the list to reach the index 3
- Here we need the 2nd index point to the item that the index 3 is points to
- In a sense we set the pointer of the 2nd item to point to the same item the the index 3 pointer is pointing to
- Once this is done, we remove the 3rd index
- The big O here is `O(n)`, because we have to iterate through items

### Finding and item in a linked list
- We can find something by its value or index
- Both for finding value and index, we need to iterate through items
- So the big O is `O(n)`
- Unlike arrays where the finding an index is `O(1)`

### Linked lists structure
- The value and the next property are called a node
- Node is an object like this:

```javascript
{
  value: 4,
  next: null // This means this is the last node
}
```

- Representing a linked list {Head -> 3 -> 8 -> 52 and tail -> 4 -> null}

```javascript

{
  Head:{
        value: 3
        next: {
                value: 8
                next: {
                         value: 52
                         next:
                              {
                                value: 4
                                next: null
                }
              }
            }
          }
// Set the tail to the next value of the 57 node 
}
```

### Linked List constructor
- The constructor of a linked list along with `push`, `unshift`, `insert` methods get passed a value.
- They also create a new node.
- In order to prevent re-writing the same code for creating a new node, we create a `Node` class.
- Whenever these methods want to create a new node they will call the `Node` class

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode; // this.head points to the newnode
    this.tail = this.head; // this.tail points to the same thing that this.head points to
    this.length = 1;
  }
}

const linked_list = new LinkedList(6);
```

### Push
- If we insert a node into an empty linked list, then both the head and tail point to it.
- Otherwise, the next property of the last node should point to the newly added node.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(6);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this; // Returning the entire linked list, instance of linkedlist which is myLinkedList
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
```

### Pop
- `Pop` the last item and move the tail to the left.
- Find the node that points to the last node.
  Set the `tail` equal to this node's next property which points to the last node.
- To access the node that points to the last node, iterate through the nodes starting from the `head`.
- Set the `next` value of the last node to `null`.
- `temp`: points to the last item.
- `pre`: points to the item before the last item, then set the `tail` equal to `pre`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.pop();
```

### Unshift
- Add a new node to the begining of the list.
- If the list is empty, then set the `tail` and `head` to point to the `new node`.
- Otherwise, set the `next` property of the `new node` to be equal to `head`.
- Then ensure `head` points to the `newly added node`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
```

### Shift
- Change the `head` to point to the `next` node.
- Remove the first item by setting it to `null`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
linked_list.shift();
```

### Get
- Use `temp` to iterate through items until it reaches the desired index.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) return undefined;
    let temp = this.head;
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
    return temp;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
linked_list.shift();
linked_list.get(1);
```

### Set
- Use `get` method to get the index, and set a new value to it.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) return undefined;
    let temp = this.head;
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
    return temp;
  }

  set(index, value) {
    let temp = this.get(index);
    if (temp) {
      temp.value = value;
      return true;
    }
    return false;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
linked_list.shift();
linked_list.get(1);
linked_list.set(2, 3);
```

### Insert

- For inserting a node to the `begining` of the list, call `unshift` method.
- For inserting a node to the `end` of the list, call `push` method.
- Otherwise, access to the `index` of the `previous element`.
- Set the `next` peroperty of the `new node` to be equal to the `next` property of the `previous node`.
- Then set the `next` property of the `previous node` to point to the `newly added node`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) return undefined;
    let temp = this.head;
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
    return temp;
  }

  set(index, value) {
    let temp = this.get(index);
    if (temp) {
      temp.value = value;
      return true;
    }
    return false;
  }

  insert(index, value) {
    if (index === 0) return this.unshift(value);
    if (index === this.length) return this.push(value);
    if (index < 0 || index > this.length) return false;

    const new_node = new Node(value);
    let temp = this.get(index - 1);
    new_node.next = temp.next;
    temp.next = new_node;
    this.length++;
    return true;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
linked_list.shift();
linked_list.get(1);
linked_list.set(2, 3);
linked_list.insert(2, 4);
```

### Remove

- For removing a node from the begining of the list, use `shift` method.
- For removing a node from the begining of the list, use `pop` method.
- Otherwise, access to the node of `previous index`.
- Set the previous node's `next` property to the `subsequent node's` `next` property.
- Set the `subsequent node's` `next` property to `null`.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) return undefined;
    let temp = this.head;
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
    return temp;
  }

  set(index, value) {
    let temp = this.get(index);
    if (temp) {
      temp.value = value;
      return true;
    }
    return false;
  }

  insert(index, value) {
    if (index === 0) return this.unshift(value);
    if (index === this.length) return this.push(value);
    if (index < 0 || index > this.length) return false;

    const new_node = new Node(value);
    let temp = this.get(index - 1);
    new_node.next = temp.next;
    temp.next = new_node;
    this.length++;
    return true;
  }

  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift(value);
    if (index === this.length - 1) return this.pop();

    let before = this.get(index - 1);
    let temp = before.next;
    before.next = temp.next;
    temp.next = null;
    this.length--;
    return temp;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.unshift(1);
linked_list.shift();
linked_list.get(1);
linked_list.set(2, 3);
linked_list.insert(2, 4);
linked_list.remove(1);
```

### Reverse

- Replace tail and head.
- `prev` is previous item which is set to null initially.
- `temp` holds the value of head.
- `next` is the subsequent node after the first node.
- In the iteration, move to next item.
- Set `this.temp` to `null` to change its direction.
- Set `prev` to `temp` to jump to the next node.
- Set `temp` to `next` to jump to the next node.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);
    this.head = newNode;
    this.tail = this.head;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop(value) {
    if (!this.head) return undefined; // no item in the linked list || null

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;
    length--;
  }

  unshift(value) {
    const new_node = new Node(value);
    if (!this.head) {
      this.head = new_node;
      this.tail = new_node;
    } else {
      new_node.next = this.head;
      this.head = new_node;
    }
    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;
    this.head = this.head.next;
    this.length--;
    if (this.length === 0) {
      this.tail = null;
    }
    temp.next = null;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) return undefined;
    let temp = this.head;
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
    return temp;
  }

  set(index, value) {
    let temp = this.get(index);
    if (temp) {
      temp.value = value;
      return true;
    }
    return false;
  }

  insert(index, value) {
    if (index === 0) return this.unshift(value);
    if (index === this.length) return this.push(value);
    if (index < 0 || index > this.length) return false;

    const new_node = new Node(value);
    let temp = this.get(index - 1);
    new_node.next = temp.next;
    temp.next = new_node;
    this.length++;
    return true;
  }

  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift(value);
    if (index === this.length - 1) return this.pop();

    let before = this.get(index - 1);
    let temp = before.next;
    before.next = temp.next;
    temp.next = null;
    this.length--;
    return temp;
  }

  reverse() {
    let temp = this.head;
    this.head = this.tail;
    this.tail = temp;
    let next = temp.next;
    let prev = null;
    for (let i = 0; i < this.length; i++) {
      next = temp.next;
      temp.next = prev;
      prev = temp;
      temp = next;
    }
    return this;
  }
}

const linked_list = new LinkedList(6);
linked_list.push(9);
linked_list.push(4);
linked_list.push(7;
linked_list.pop(2);
linked_list.unshift(1);
linked_list.shift();
linked_list.get(1);
linked_list.set(2, 3);
linked_list.insert(2, 4);
linked_list.remove(1);
linked_list.reverse();
```
