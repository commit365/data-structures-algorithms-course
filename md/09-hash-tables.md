# Lesson 9: Hash Tables

## 9.1 Introduction to Hash Tables

A **hash table** (or hash map) is a data structure that provides a way to store and retrieve data efficiently using key-value pairs. It uses a hash function to compute an index (or hash code) into an array of buckets or slots, from which the desired value can be found.

### 9.1.1 Significance of Hash Tables
Hash tables are significant in data retrieval for several reasons:

- **Fast Access**: Hash tables provide average-case constant time complexity, O(1), for search, insert, and delete operations. This makes them highly efficient for scenarios where quick data retrieval is essential.
- **Dynamic Size**: Hash tables can dynamically resize as the number of entries grows, allowing for efficient memory usage.
- **Flexible Keys**: They allow for various data types to be used as keys, making them versatile for different applications.

### 9.1.2 Basic Operations
The primary operations performed on hash tables include:

- **Insertion**: Adding a new key-value pair to the hash table.
- **Deletion**: Removing a key-value pair from the hash table.
- **Search**: Retrieving the value associated with a specific key.

## 9.2 Collision Resolution Techniques

A collision occurs when two keys hash to the same index in the hash table. To handle collisions, various resolution techniques can be employed:

### 9.2.1 Chaining
Chaining is a collision resolution technique where each bucket in the hash table contains a linked list (or another data structure) of all entries that hash to the same index. When a collision occurs, the new entry is simply added to the linked list.

#### Example of Chaining Implementation
```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None  # Pointer to the next node

class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Initialize hash table with empty buckets

    def hash_function(self, key):
        return hash(key) % self.size  # Compute hash index

    def insert(self, key, value):
        index = self.hash_function(key)
        new_node = Node(key, value)
        if self.table[index] is None:
            self.table[index] = new_node  # Insert new node if bucket is empty
        else:
            # Collision occurred; add to the linked list
            current = self.table[index]
            while current:
                if current.key == key:
                    current.value = value  # Update value if key exists
                    return
                if current.next is None:
                    break
                current = current.next
            current.next = new_node  # Add new node to the end of the list

    def search(self, key):
        index = self.hash_function(key)
        current = self.table[index]
        while current:
            if current.key == key:
                return current.value  # Return value if key is found
            current = current.next
        return None  # Key not found

    def delete(self, key):
        index = self.hash_function(key)
        current = self.table[index]
        prev = None
        while current:
            if current.key == key:
                if prev:
                    prev.next = current.next  # Bypass the node to delete it
                else:
                    self.table[index] = current.next  # Update head if deleting first node
                return
            prev = current
            current = current.next
```

### 9.2.2 Open Addressing
Open addressing is another collision resolution technique where all elements are stored in the hash table itself. When a collision occurs, the algorithm probes the table for the next available slot using a predefined probing sequence.

#### Common Probing Techniques
- **Linear Probing**: Check the next slot sequentially until an empty slot is found.
- **Quadratic Probing**: Use a quadratic function to find the next slot.
- **Double Hashing**: Use a second hash function to determine the step size for probing.

#### Example of Linear Probing Implementation
```python
class OpenAddressingHashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Initialize hash table with empty slots

    def hash_function(self, key):
        return hash(key) % self.size  # Compute hash index

    def insert(self, key, value):
        index = self.hash_function(key)
        while self.table[index] is not None:
            if self.table[index][0] == key:
                self.table[index] = (key, value)  # Update value if key exists
                return
            index = (index + 1) % self.size  # Linear probing
        self.table[index] = (key, value)  # Insert new key-value pair

    def search(self, key):
        index = self.hash_function(key)
        while self.table[index] is not None:
            if self.table[index][0] == key:
                return self.table[index][1]  # Return value if key is found
            index = (index + 1) % self.size  # Linear probing
        return None  # Key not found

    def delete(self, key):
        index = self.hash_function(key)
        while self.table[index] is not None:
            if self.table[index][0] == key:
                self.table[index] = None  # Mark slot as deleted
                return
            index = (index + 1) % self.size  # Linear probing
```

## 9.3 Performance Analysis

### 9.3.1 Time Complexity
The average-case time complexity for search, insert, and delete operations in a hash table is O(1) when using chaining or open addressing with a good hash function. However, the worst-case time complexity can degrade to O(n) if many collisions occur (e.g., if all keys hash to the same index).

### 9.3.2 Load Factor
The **load factor** is defined as the number of entries in the hash table divided by the number of buckets. A higher load factor increases the chance of collisions and can degrade performance. To maintain efficiency, hash tables are often resized (rehashing) when the load factor exceeds a certain threshold (commonly 0.7).

### 9.3.3 Space Complexity
The space complexity of a hash table is O(n), where n is the number of entries. However, the actual space used may be larger due to the need for empty slots in open addressing or linked lists in chaining.

This lesson introduced hash tables, their significance in data retrieval, and collision resolution techniques such as chaining and open addressing. You also learned about performance analysis, including time complexity, load factor, and space complexity, which are crucial for understanding the efficiency of hash tables in various applications.