# Lesson 11: Balanced Trees

Balanced trees are a type of binary tree that maintains a specific balance condition to ensure that the height of the tree remains logarithmic relative to the number of nodes. This property allows for efficient searching, insertion, and deletion operations. In this lesson, we will explore several types of balanced trees, including AVL trees, Red-Black trees, B-trees, and Splay trees.

## 11.1 Understanding Balanced Trees

### 11.1.1 AVL Trees
An **AVL tree** is a self-balancing binary search tree where the difference in heights between the left and right subtrees (the balance factor) of any node is at most 1. This ensures that the tree remains balanced, leading to O(log n) time complexity for search, insert, and delete operations.

#### Balance Factor
- The balance factor is calculated as:
  $$
  \text{Balance Factor} = \text{Height of Left Subtree} - \text{Height of Right Subtree}
  $$

### 11.1.2 Red-Black Trees
A **Red-Black tree** is another type of self-balancing binary search tree that maintains balance through specific properties:
1. Each node is either red or black.
2. The root is always black.
3. Red nodes cannot have red children (no two reds in a row).
4. Every path from a node to its descendant leaves must have the same number of black nodes.

These properties ensure that the longest path from the root to a leaf is no more than twice the length of the shortest path, maintaining O(log n) time complexity for operations.

### 11.1.3 B-Trees
A **B-tree** is a self-balancing tree data structure that maintains sorted data and allows for efficient insertion, deletion, and search operations. B-trees are commonly used in databases and file systems due to their ability to handle large amounts of data.

#### Properties of B-Trees
- Each node can have multiple children (more than two).
- All leaves are at the same level.
- A B-tree of order m can have at most m children and at least ⌈m/2⌉ children.

### 11.1.4 Splay Trees
A **Splay tree** is a self-adjusting binary search tree that moves frequently accessed elements closer to the root through a process called splaying. This allows for efficient access to recently accessed nodes.

#### Splaying Operation
Splaying can be performed using three rotations:
1. **Zig**: A single rotation when the node is a child of the root.
2. **Zig-Zig**: A double rotation when the node is a left child of a left child or a right child of a right child.
3. **Zig-Zag**: A double rotation when the node is a left child of a right child or a right child of a left child.

## 11.2 Operations and Balancing Techniques

### 11.2.1 AVL Trees Operations
- **Insertion**: After inserting a node, check the balance factor of each ancestor node. If the balance factor becomes greater than 1 or less than -1, perform rotations to restore balance.
  - **Single Rotations**: Left or right rotations.
  - **Double Rotations**: Left-Right or Right-Left rotations.

- **Deletion**: Similar to insertion, after deleting a node, check the balance factor and perform rotations as needed.

### 11.2.2 Red-Black Trees Operations
- **Insertion**: Insert the new node as you would in a regular binary search tree. Then, fix any violations of the Red-Black properties by recoloring and performing rotations as necessary.
- **Deletion**: Deletion is more complex, as it may require multiple rotations and recoloring to maintain the properties.

### 11.2.3 B-Trees Operations
- **Insertion**: Insert keys into the appropriate leaf node. If the node exceeds its maximum number of keys, split the node and promote the middle key to the parent.
- **Deletion**: Deleting a key may require merging nodes or redistributing keys among siblings to maintain the properties of the B-tree.

### 11.2.4 Splay Trees Operations
- **Insertion**: Insert the node as you would in a regular binary search tree, then splay it to the root.
- **Deletion**: Splay the node to be deleted to the root, then remove it and splay the last accessed node to the root.

## 11.3 Performance Comparisons

### 11.3.1 Time Complexity
- **AVL Trees**: O(log n) for search, insert, and delete due to strict balancing.
- **Red-Black Trees**: O(log n) for search, insert, and delete due to less strict balancing compared to AVL trees.
- **B-Trees**: O(log n) for search, insert, and delete, with better performance for disk-based storage due to fewer accesses.
- **Splay Trees**: O(log n) amortized time for search, insert, and delete, but O(n) in the worst case.

### 11.3.2 Space Complexity
All the balanced trees typically have a space complexity of O(n), where n is the number of nodes in the tree.

### 11.3.3 Use Cases
- **AVL Trees**: Suitable for applications requiring frequent insertions and deletions while maintaining sorted order, such as memory management.
- **Red-Black Trees**: Often used in implementations of associative arrays and in the standard libraries of many programming languages due to their balance and efficiency.
- **B-Trees**: Commonly used in databases and filesystems where large blocks of data are read and written.
- **Splay Trees**: Useful in scenarios where certain elements are accessed more frequently, allowing for faster access to those elements over time.

This lesson provided an overview of balanced trees, including AVL trees, Red-Black trees, B-trees, and Splay trees. You learned about their operations, balancing techniques, and performance comparisons, highlighting the importance of balanced trees in maintaining efficient data structures for various applications.