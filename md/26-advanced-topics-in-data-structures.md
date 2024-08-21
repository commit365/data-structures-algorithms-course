# Lesson 26: Advanced Topics in Data Structures

Advanced data structures provide efficient ways to store and manipulate data, often optimizing specific operations that are common in various applications. In this lesson, we will introduce several advanced data structures, including tries, segment trees, Fenwick trees, and disjoint set union (DSU). We will also explore their applications and use cases in competitive programming and real-world scenarios.

## 26.1 Introduction to Advanced Data Structures

### 26.1.1 Tries
A **trie** (pronounced "try") is a tree-like data structure used to store a dynamic set of strings, where each node represents a character of a string. Tries are particularly useful for tasks involving prefix matching, such as autocomplete and spell checking.

#### Characteristics
- Each path down the tree represents a prefix of one or more strings.
- The root node represents an empty string, and each edge represents a character.
- Each node can store a boolean value indicating whether it marks the end of a valid string.

#### Implementation
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word

    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

### 26.1.2 Segment Trees
A **segment tree** is a binary tree used for storing intervals or segments. It allows querying the sum, minimum, maximum, or other associative operations over a range of values efficiently.

#### Characteristics
- Each node represents an interval, and the leaves represent individual elements.
- The tree is built in a way that allows for efficient updates and queries.

#### Implementation
```python
class SegmentTree:
    def __init__(self, data):
        self.n = len(data)
        self.tree = [0] * (2 * self.n)
        self.build(data)

    def build(self, data):
        # Build the tree
        for i in range(self.n):
            self.tree[self.n + i] = data[i]
        for i in range(self.n - 1, 0, -1):
            self.tree[i] = self.tree[i * 2] + self.tree[i * 2 + 1]  # Sum of children

    def update(self, index, value):
        # Update the value at index
        index += self.n
        self.tree[index] = value
        while index > 1:
            index //= 2
            self.tree[index] = self.tree[index * 2] + self.tree[index * 2 + 1]

    def query(self, left, right):
        # Query the sum in the interval [left, right)
        result = 0
        left += self.n
        right += self.n
        while left < right:
            if left % 2 == 1:
                result += self.tree[left]
                left += 1
            if right % 2 == 1:
                right -= 1
                result += self.tree[right]
            left //= 2
            right //= 2
        return result
```

### 26.1.3 Fenwick Trees (Binary Indexed Trees)
A **Fenwick tree** (or Binary Indexed Tree) is a data structure that provides efficient methods for cumulative frequency tables and point updates. It allows for both prefix sum queries and updates in logarithmic time.

#### Characteristics
- Uses a binary representation of indices to navigate through the tree.
- Efficient for dynamic cumulative frequency calculations.

#### Implementation
```python
class FenwickTree:
    def __init__(self, size):
        self.size = size
        self.tree = [0] * (size + 1)

    def update(self, index, value):
        while index <= self.size:
            self.tree[index] += value
            index += index & -index  # Move to the next index

    def query(self, index):
        sum_ = 0
        while index > 0:
            sum_ += self.tree[index]
            index -= index & -index  # Move to the parent index
        return sum_
```

### 26.1.4 Disjoint Set Union (DSU)
The **Disjoint Set Union** (also known as Union-Find) is a data structure that keeps track of a partition of a set into disjoint (non-overlapping) subsets. It supports two primary operations: **union** (to merge two sets) and **find** (to determine which set a particular element belongs to).

#### Characteristics
- Efficiently handles dynamic connectivity queries.
- Often used in algorithms like Kruskal's for finding the Minimum Spanning Tree.

#### Implementation
```python
class DisjointSet:
    def __init__(self, size):
        self.parent = list(range(size))
        self.rank = [1] * size

    def find(self, item):
        if self.parent[item] != item:
            self.parent[item] = self.find(self.parent[item])  # Path compression
        return self.parent[item]

    def union(self, set1, set2):
        root1 = self.find(set1)
        root2 = self.find(set2)

        if root1 != root2:
            # Union by rank
            if self.rank[root1] > self.rank[root2]:
                self.parent[root2] = root1
            elif self.rank[root1] < self.rank[root2]:
                self.parent[root1] = root2
            else:
                self.parent[root2] = root1
                self.rank[root1] += 1
```

## 26.2 Applications and Use Cases for Advanced Data Structures

### 26.2.1 Competitive Programming
Advanced data structures are frequently used in competitive programming to solve complex problems efficiently. For example:
- **Tries** are used for string matching problems and autocomplete features.
- **Segment trees** and **Fenwick trees** are used for range queries and updates in problems involving arrays.
- **Disjoint Set Union (DSU)** is used in problems involving connectivity and clustering.

### 26.2.2 Real-World Applications
- **Tries**: Used in search engines for prefix searching and in networking for routing table management.
- **Segment Trees**: Used in applications requiring dynamic range queries, such as stock price analysis and image processing.
- **Fenwick Trees**: Used in applications requiring cumulative frequency tables, such as in data analytics and statistics.
- **Disjoint Set Union (DSU)**: Used in network connectivity problems, image processing (connected components), and clustering algorithms.

### 26.2.3 Data Compression
- **Huffman coding** (related to tries) is used in data compression algorithms to efficiently encode data based on frequency.

### 26.2.4 Game Development
- Advanced data structures can be used in game development for pathfinding algorithms, collision detection, and managing game states.

## 26.3 Summary

This lesson introduced several advanced data structures, including tries, segment trees, Fenwick trees, and disjoint set union (DSU). We explored their characteristics, implementations, and applications in competitive programming and real-world scenarios. Understanding these advanced data structures is essential for solving complex problems efficiently and effectively in various domains of computer science and programming.