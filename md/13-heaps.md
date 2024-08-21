# Lesson 13: Heaps

## 13.1 Understanding Heap Data Structures

A **heap** is a specialized tree-based data structure that satisfies the **heap property**. Heaps are commonly used to implement priority queues and are essential in various algorithms, including heap sort.

### 13.1.1 Properties of Heaps
- **Complete Binary Tree**: A heap is always a complete binary tree, meaning all levels are fully filled except possibly for the last level, which is filled from left to right.
- **Heap Property**: 
  - In a **min-heap**, the value of each node is greater than or equal to the value of its parent. The minimum element is at the root.
  - In a **max-heap**, the value of each node is less than or equal to the value of its parent. The maximum element is at the root.

### 13.1.2 Applications of Heaps
- **Priority Queues**: Heaps are commonly used to implement priority queues, where elements are processed based on their priority rather than their order of arrival.
- **Heap Sort**: A sorting algorithm that uses a heap to sort elements in O(n log n) time.
- **Graph Algorithms**: Heaps are used in algorithms like Dijkstra's and Prim's for efficiently retrieving the minimum or maximum elements.

## 13.2 Implementation of Heaps

Heaps can be implemented using arrays or linked structures, but the most common implementation is using arrays due to its efficiency in space and access time.

### 13.2.1 Min-Heap Implementation
In a min-heap, the parent node is always less than or equal to its children. The following is an implementation of a min-heap using an array.

#### Min-Heap Class
```python
class MinHeap:
    def __init__(self):
        self.heap = []  # Initialize an empty heap

    def parent(self, index):
        return (index - 1) // 2  # Get the index of the parent

    def left_child(self, index):
        return 2 * index + 1  # Get the index of the left child

    def right_child(self, index):
        return 2 * index + 2  # Get the index of the right child

    def insert(self, value):
        self.heap.append(value)  # Add the new value to the end of the heap
        self._heapify_up(len(self.heap) - 1)  # Restore heap property

    def _heapify_up(self, index):
        while index > 0 and self.heap[index] < self.heap[self.parent(index)]:
            # Swap if the current node is less than its parent
            self.heap[index], self.heap[self.parent(index)] = self.heap[self.parent(index)], self.heap[index]
            index = self.parent(index)  # Move up to the parent's index

    def extract_min(self):
        if len(self.heap) == 0:
            raise Exception("Heap is empty")
        if len(self.heap) == 1:
            return self.heap.pop()  # Remove and return the only element
        root = self.heap[0]  # Store the root value
        self.heap[0] = self.heap.pop()  # Replace root with the last element
        self._heapify_down(0)  # Restore heap property
        return root

    def _heapify_down(self, index):
        smallest = index
        left = self.left_child(index)
        right = self.right_child(index)

        if left < len(self.heap) and self.heap[left] < self.heap[smallest]:
            smallest = left
        if right < len(self.heap) and self.heap[right] < self.heap[smallest]:
            smallest = right

        if smallest != index:
            # Swap and continue heapifying down
            self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index]
            self._heapify_down(smallest)

    def get_min(self):
        if len(self.heap) == 0:
            raise Exception("Heap is empty")
        return self.heap[0]  # Return the root value
```

### 13.2.2 Max-Heap Implementation
In a max-heap, the parent node is always greater than or equal to its children. The implementation is similar to that of a min-heap, with adjustments in the comparison logic.

#### Max-Heap Class
```python
class MaxHeap:
    def __init__(self):
        self.heap = []  # Initialize an empty heap

    def parent(self, index):
        return (index - 1) // 2  # Get the index of the parent

    def left_child(self, index):
        return 2 * index + 1  # Get the index of the left child

    def right_child(self, index):
        return 2 * index + 2  # Get the index of the right child

    def insert(self, value):
        self.heap.append(value)  # Add the new value to the end of the heap
        self._heapify_up(len(self.heap) - 1)  # Restore heap property

    def _heapify_up(self, index):
        while index > 0 and self.heap[index] > self.heap[self.parent(index)]:
            # Swap if the current node is greater than its parent
            self.heap[index], self.heap[self.parent(index)] = self.heap[self.parent(index)], self.heap[index]
            index = self.parent(index)  # Move up to the parent's index

    def extract_max(self):
        if len(self.heap) == 0:
            raise Exception("Heap is empty")
        if len(self.heap) == 1:
            return self.heap.pop()  # Remove and return the only element
        root = self.heap[0]  # Store the root value
        self.heap[0] = self.heap.pop()  # Replace root with the last element
        self._heapify_down(0)  # Restore heap property
        return root

    def _heapify_down(self, index):
        largest = index
        left = self.left_child(index)
        right = self.right_child(index)

        if left < len(self.heap) and self.heap[left] > self.heap[largest]:
            largest = left
        if right < len(self.heap) and self.heap[right] > self.heap[largest]:
            largest = right

        if largest != index:
            # Swap and continue heapifying down
            self.heap[index], self.heap[largest] = self.heap[largest], self.heap[index]
            self._heapify_down(largest)

    def get_max(self):
        if len(self.heap) == 0:
            raise Exception("Heap is empty")
        return self.heap[0]  # Return the root value
```

### 13.2.3 Priority Queue Implementation
A priority queue can be implemented using either a min-heap or a max-heap. In a priority queue, elements are dequeued based on their priority rather than their order of arrival.

#### Example of a Priority Queue Using a Min-Heap
```python
class PriorityQueue:
    def __init__(self):
        self.min_heap = MinHeap()  # Use min-heap for priority queue

    def enqueue(self, priority, value):
        self.min_heap.insert((priority, value))  # Insert as a tuple (priority, value)

    def dequeue(self):
        if self.min_heap.is_empty():
            raise Exception("Priority queue is empty")
        return self.min_heap.extract_min()[1]  # Extract and return the value

    def peek(self):
        if self.min_heap.is_empty():
            raise Exception("Priority queue is empty")
        return self.min_heap.get_min()[1]  # Return the value with the highest priority
```

## 13.3 Heap Sort

Heap sort is a comparison-based sorting algorithm that utilizes the heap data structure. It involves two main phases: building a heap from the input data and then repeatedly extracting the maximum (or minimum) element from the heap to produce a sorted array.

### 13.3.1 Heap Sort Algorithm Steps
1. **Build a Max-Heap** from the input data.
2. **Extract the Maximum** element from the heap and place it at the end of the array.
3. **Reduce the Size of the Heap** by one and call the heapify function to maintain the heap property.
4. Repeat steps 2 and 3 until all elements are sorted.

### 13.3.2 Heap Sort Implementation
```python
def heapify(arr, n, i):
    largest = i  # Initialize largest as root
    left = 2 * i + 1  # Left child index
    right = 2 * i + 2  # Right child index

    # Check if left child exists and is greater than root
    if left < n and arr[left] > arr[largest]:
        largest = left

    # Check if right child exists and is greater than largest so far
    if right < n and arr[right] > arr[largest]:
        largest = right

    # If largest is not root, swap and continue heapifying
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]  # Swap
        heapify(arr, n, largest)

def heap_sort(arr):
    n = len(arr)

    # Build a max-heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements from the heap one by one
    for i in range(n - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]  # Swap
        heapify(arr, i, 0)  # Heapify the root element

# Example usage
arr = [12, 11, 13, 5, 6, 7]
heap_sort(arr)
print("Sorted array is:", arr)  # Output: Sorted array is: [5, 6, 7, 11, 12, 13]
```

This lesson covered heaps, including their properties, implementations of min-heaps and max-heaps, and their use in priority queues and heap sort. Understanding heaps is crucial for efficiently managing and organizing data in various applications, particularly when priority and order matter.