# Lesson 8: Queues

## 8.1 Understanding Queue Data Structures

A **queue** is a linear data structure that follows the **First In, First Out (FIFO)** principle. This means that the first element added to the queue will be the first one to be removed. Queues are widely used in various applications where order matters.

### 8.1.1 Characteristics of Queues
- **Enqueue**: The operation of adding an element to the back of the queue.
- **Dequeue**: The operation of removing an element from the front of the queue.
- **Front**: The operation to view the front element without removing it.
- **IsEmpty**: A check to determine if the queue is empty.

### 8.1.2 Types of Queues
- **Simple Queue**: A basic queue that follows the FIFO principle.
- **Circular Queue**: A queue where the last position is connected back to the first position, allowing for efficient use of space.
- **Priority Queue**: A special type of queue where each element has a priority. Elements with higher priority are dequeued before elements with lower priority, regardless of their order in the queue.

## 8.2 Implementation of Queues

Queues can be implemented using various data structures, including lists and linked lists. Below, we will explore both implementations.

### 8.2.1 Queue Implementation Using Lists
Python's built-in list can be used to implement a simple queue. The `append()` method is used to enqueue elements, and the `pop(0)` method is used to dequeue elements.

#### Queue Class Using List
```python
class Queue:
    def __init__(self):
        self.items = []  # Initialize an empty list to store queue items

    def is_empty(self):
        return len(self.items) == 0  # Check if the queue is empty

    def enqueue(self, item):
        self.items.append(item)  # Add an item to the back of the queue

    def dequeue(self):
        if self.is_empty():
            raise Exception("Queue is empty")
        return self.items.pop(0)  # Remove and return the front item

    def front(self):
        if self.is_empty():
            raise Exception("Queue is empty")
        return self.items[0]  # Return the front item without removing it

    def size(self):
        return len(self.items)  # Return the number of items in the queue
```

#### Example Usage
```python
queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)
print(queue.dequeue())  # Output: 1
print(queue.front())     # Output: 2
print(queue.size())      # Output: 2
```

### 8.2.2 Queue Implementation Using Linked Lists
Queues can also be implemented using linked lists. In this implementation, the front of the queue is represented by the head of the linked list, and the back of the queue is represented by the tail.

#### Node Class
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.next = None  # Pointer to the next node
```

#### Queue Class Using Linked List
```python
class LinkedListQueue:
    def __init__(self):
        self.head = None  # Initialize the head of the linked list
        self.tail = None  # Initialize the tail of the linked list

    def is_empty(self):
        return self.head is None  # Check if the queue is empty

    def enqueue(self, item):
        new_node = Node(item)  # Create a new node
        if self.tail:  # If the queue is not empty
            self.tail.next = new_node  # Point the current tail to the new node
        self.tail = new_node  # Update the tail to the new node
        if self.head is None:  # If the queue was empty
            self.head = new_node  # Set the head to the new node

    def dequeue(self):
        if self.is_empty():
            raise Exception("Queue is empty")
        dequeued_node = self.head  # Store the current head
        self.head = self.head.next  # Update the head to the next node
        if self.head is None:  # If the queue is now empty
            self.tail = None  # Set the tail to None
        return dequeued_node.data  # Return the data of the dequeued node

    def front(self):
        if self.is_empty():
            raise Exception("Queue is empty")
        return self.head.data  # Return the data of the head node

    def size(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count  # Return the number of items in the queue
```

#### Example Usage
```python
linked_queue = LinkedListQueue()
linked_queue.enqueue(1)
linked_queue.enqueue(2)
linked_queue.enqueue(3)
print(linked_queue.dequeue())  # Output: 1
print(linked_queue.front())     # Output: 2
print(linked_queue.size())      # Output: 2
```

## 8.3 Applications of Queues

Queues have several practical applications, including:

### 8.3.1 Scheduling
Queues are often used in scheduling tasks, such as managing processes in operating systems. For example, when multiple processes are waiting for CPU time, they are placed in a queue, and the CPU processes them in the order they arrive.

### 8.3.2 Buffering
Queues are used in buffering scenarios, such as in IO operations. When data is being transferred between devices, a queue can hold the data temporarily until it is processed.

### 8.3.3 Print Queue
In print spooling, documents sent to a printer are stored in a queue. The printer processes the documents in the order they were received, ensuring that the first document sent to the printer is the first one printed.

### 8.3.4 Breadth-First Search (BFS)
Queues are used in graph algorithms like Breadth-First Search (BFS) to explore nodes level by level. Nodes are added to the queue as they are discovered, and the algorithm processes each node in the order they were added.

This lesson covered the understanding of queue data structures, their types, and their implementation using lists and linked lists. Additionally, you learned about practical applications of queues in scheduling, buffering, and other scenarios, highlighting their importance in programming and computer science.

[Next: 09. Hash Tables](./09-hash-tables.md)