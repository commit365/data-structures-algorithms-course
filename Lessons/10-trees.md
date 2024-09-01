# Lesson 10: Trees

## 10.1 Overview of Tree Data Structures

A **tree** is a hierarchical data structure that consists of nodes connected by edges. It is used to represent relationships between data in a parent-child hierarchy. Trees are widely used in computer science for various applications, such as organizing data, managing hierarchical structures, and facilitating efficient searching and sorting.

### 10.1.1 Terminology
- **Node**: The fundamental part of a tree that contains data and may link to other nodes.
- **Root**: The top node in a tree, which has no parent.
- **Child**: A node that is a descendant of another node.
- **Parent**: A node that has one or more children.
- **Leaf**: A node that does not have any children.
- **Subtree**: A tree formed by a node and its descendants.
- **Height**: The length of the longest path from a node to its leaf nodes.
- **Depth**: The length of the path from the root to a specific node.

### 10.1.2 Properties of Trees
- **Acyclic**: Trees do not contain cycles; there is exactly one path between any two nodes.
- **Connected**: All nodes are connected through edges.
- **N nodes**: A tree with N nodes has exactly N-1 edges.

## 10.2 Introduction to Binary Trees

A **binary tree** is a type of tree where each node has at most two children, referred to as the left child and the right child. Binary trees are widely used due to their simplicity and efficiency in various applications.

### 10.2.1 Types of Binary Trees
- **Full Binary Tree**: Every node has either 0 or 2 children.
- **Complete Binary Tree**: All levels are fully filled except possibly for the last level, which is filled from left to right.
- **Perfect Binary Tree**: All internal nodes have two children, and all leaf nodes are at the same level.
- **Balanced Binary Tree**: The height of the left and right subtrees of any node differ by at most one.

### 10.2.2 Basic Operations on Binary Trees
- **Insertion**: Adding a new node to the tree.
- **Deletion**: Removing a node from the tree.
- **Traversal**: Visiting all nodes in the tree in a specific order (in-order, pre-order, post-order, level-order).

#### Example of Binary Tree Node Structure
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data part
        self.left = None  # Pointer to the left child
        self.right = None  # Pointer to the right child
```

## 10.3 Introduction to Binary Search Trees (BST)

A **binary search tree (BST)** is a special type of binary tree that maintains a specific order. In a BST:
- The left subtree of a node contains only nodes with values less than the node's value.
- The right subtree of a node contains only nodes with values greater than the node's value.
- Both the left and right subtrees must also be binary search trees.

### 10.3.1 Properties of BST
- **Ordered Structure**: This property allows for efficient searching, insertion, and deletion operations.
- **Average Time Complexity**: The average time complexity for search, insert, and delete operations in a BST is O(log n), where n is the number of nodes. However, in the worst case (e.g., a degenerate tree), it can degrade to O(n).

### 10.3.2 Basic Operations on BST
- **Insertion**: Insert a new node while maintaining the BST properties.
- **Deletion**: Remove a node while ensuring the BST properties are preserved.
- **Searching**: Find a node in the tree.

#### Example of Insertion in a BST
```python
class BinarySearchTree:
    def __init__(self):
        self.root = None  # Initialize the root of the tree

    def insert(self, data):
        if self.root is None:
            self.root = Node(data)  # Create a new node if the tree is empty
        else:
            self._insert_recursive(self.root, data)  # Call the recursive helper function

    def _insert_recursive(self, node, data):
        if data < node.data:  # If data is less, go to the left subtree
            if node.left is None:
                node.left = Node(data)  # Insert new node
            else:
                self._insert_recursive(node.left, data)  # Recur down the left subtree
        else:  # If data is greater, go to the right subtree
            if node.right is None:
                node.right = Node(data)  # Insert new node
            else:
                self._insert_recursive(node.right, data)  # Recur down the right subtree
```

### 10.3.3 Searching in a BST
```python
def search(self, data):
    return self._search_recursive(self.root, data)

def _search_recursive(self, node, data):
    if node is None or node.data == data:  # Base case: found or reached a leaf
        return node
    if data < node.data:  # If data is less, search in the left subtree
        return self._search_recursive(node.left, data)
    return self._search_recursive(node.right, data)  # Search in the right subtree
```

### 10.3.4 Applications of Binary Search Trees
- **Searching**: Efficiently find elements in a dataset.
- **Dynamic Set Operations**: Insertions and deletions can be performed efficiently.
- **Sorting**: In-order traversal of a BST produces sorted data.
- **Range Queries**: Efficiently find all keys within a given range.

This lesson provided an overview of tree data structures, including terminology and properties, as well as an introduction to binary trees and binary search trees (BST). You also learned about basic operations on these trees and their applications, highlighting the importance of trees in organizing and managing data efficiently.

[Next: 11. Balanced Trees](./11-balanced-trees.md)