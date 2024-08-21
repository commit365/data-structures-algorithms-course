# Lesson 6: Linked Lists

## 6.1 Introduction to Linked Lists

A **linked list** is a linear data structure where elements, called nodes, are stored in a sequence. Unlike arrays, linked lists do not require contiguous memory locations; each node points to the next node in the sequence, allowing for dynamic memory allocation. There are several types of linked lists, including singly linked lists, doubly linked lists, and circular linked lists.

### 6.1.1 Singly Linked Lists
A **singly linked list** consists of nodes where each node contains two components: data and a pointer (or reference) to the next node in the sequence. The first node is called the head, and the last node points to `None`, indicating the end of the list.

#### Structure of a Singly Linked List Node
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.next = None  # Pointer to the next node
```

### 6.1.2 Doubly Linked Lists
A **doubly linked list** consists of nodes where each node contains three components: data, a pointer to the next node, and a pointer to the previous node. This allows traversal in both directions.

#### Structure of a Doubly Linked List Node
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.next = None  # Pointer to the next node
        self.prev = None  # Pointer to the previous node
```

### 6.1.3 Circular Linked Lists
A **circular linked list** can be either singly or doubly linked, but the last node points back to the first node instead of pointing to `None`. This creates a circular structure, allowing for continuous traversal.

#### Structure of a Circular Singly Linked List Node
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.next = None  # Pointer to the next node
```

## 6.2 Operations on Linked Lists

### 6.2.1 Insertion
Insertion in a linked list can occur at different positions: at the beginning, at the end, or at a specific index.

#### Inserting at the Beginning
```python
def insert_at_beginning(head, new_data):
    new_node = Node(new_data)
    new_node.next = head  # Point new node to the current head
    return new_node  # Return new head
```

#### Inserting at the End
```python
def insert_at_end(head, new_data):
    new_node = Node(new_data)
    if head is None:
        return new_node  # If the list is empty, return new node
    last_node = head
    while last_node.next:
        last_node = last_node.next  # Traverse to the last node
    last_node.next = new_node  # Point last node to new node
    return head
```

#### Inserting at a Specific Position
```python
def insert_at_position(head, new_data, position):
    new_node = Node(new_data)
    if position == 0:
        return insert_at_beginning(head, new_data)
    current = head
    for _ in range(position - 1):
        if current is None:
            raise Exception("Position out of bounds")
        current = current.next
    new_node.next = current.next
    current.next = new_node
    return head
```

### 6.2.2 Deletion
Deletion can also occur at different positions: from the beginning, from the end, or from a specific index.

#### Deleting from the Beginning
```python
def delete_from_beginning(head):
    if head is None:
        return None  # If the list is empty
    return head.next  # Return the new head
```

#### Deleting from the End
```python
def delete_from_end(head):
    if head is None:
        return None  # If the list is empty
    if head.next is None:
        return None  # If there's only one node
    second_last = head
    while second_last.next.next:
        second_last = second_last.next  # Traverse to the second last node
    second_last.next = None  # Remove the last node
    return head
```

#### Deleting from a Specific Position
```python
def delete_from_position(head, position):
    if head is None:
        return None
    if position == 0:
        return delete_from_beginning(head)
    current = head
    for _ in range(position - 1):
        if current is None or current.next is None:
            raise Exception("Position out of bounds")
        current = current.next
    current.next = current.next.next  # Bypass the node to be deleted
    return head
```

### 6.2.3 Traversal
Traversal is the process of visiting each node in the linked list. You can traverse a linked list using a simple loop.

```python
def traverse(head):
    current = head
    while current:
        print(current.data, end=" -> ")
        current = current.next
    print("None")  # Indicate the end of the list
```

### 6.2.4 Applications of Linked Lists
Linked lists have several applications, including:

- **Dynamic Memory Allocation**: Linked lists allow for dynamic memory allocation, making them suitable for applications where the size of the data structure is unknown at compile time.
- **Implementing Stacks and Queues**: Linked lists can be used to implement stack and queue data structures, providing efficient insertion and deletion.
- **Graph Representation**: Linked lists can represent adjacency lists in graph data structures, allowing for efficient traversal of graph nodes.
- **Undo Functionality in Applications**: Linked lists can be used to implement undo functionality in applications, where each action is stored as a node in the list.

This lesson covered the introduction to linked lists, including singly, doubly, and circular linked lists, as well as basic operations such as insertion, deletion, traversal, and their applications. Understanding linked lists is essential for mastering more complex data structures and algorithms.