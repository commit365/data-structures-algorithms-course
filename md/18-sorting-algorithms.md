# Lesson 18: Sorting Algorithms

Sorting algorithms are fundamental algorithms in computer science used to arrange the elements of a list or array in a specific order, typically in ascending or descending order. This lesson provides an overview of common sorting algorithms, including bubble sort, selection sort, insertion sort, merge sort, quicksort, heapsort, and radix sort. We will also conduct a comparative analysis of these algorithms based on their time and space complexity.

## 18.1 Overview of Common Sorting Algorithms

### 18.1.1 Bubble Sort
**Bubble sort** is a simple comparison-based sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The process is repeated until no swaps are needed, indicating that the list is sorted.

#### Implementation
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]  # Swap
```

### 18.1.2 Selection Sort
**Selection sort** works by dividing the list into a sorted and an unsorted region. It repeatedly selects the smallest (or largest) element from the unsorted region and moves it to the end of the sorted region.

#### Implementation
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_index = i
        for j in range(i+1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]  # Swap
```

### 18.1.3 Insertion Sort
**Insertion sort** builds a sorted array one element at a time. It takes each element from the unsorted portion and inserts it into the correct position in the sorted portion.

#### Implementation
```python
def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]  # Shift elements
            j -= 1
        arr[j + 1] = key  # Insert key
```

### 18.1.4 Merge Sort
**Merge sort** is a divide-and-conquer algorithm that divides the array into halves, recursively sorts each half, and then merges the sorted halves back together.

#### Implementation
```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2  # Find the middle point
        left_half = arr[:mid]  # Divide the array elements
        right_half = arr[mid:]

        merge_sort(left_half)  # Sort the first half
        merge_sort(right_half)  # Sort the second half

        i = j = k = 0

        # Copy data to temp arrays L[] and R[]
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        # Checking if any element was left
        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1
```

### 18.1.5 Quicksort
**Quicksort** is a divide-and-conquer algorithm that selects a 'pivot' element and partitions the array into two sub-arrays according to whether the elements are less than or greater than the pivot. The sub-arrays are then sorted recursively.

#### Implementation
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr  # Base case
    pivot = arr[len(arr) // 2]  # Choose pivot
    left = [x for x in arr if x < pivot]  # Elements less than pivot
    middle = [x for x in arr if x == pivot]  # Elements equal to pivot
    right = [x for x in arr if x > pivot]  # Elements greater than pivot
    return quicksort(left) + middle + quicksort(right)  # Recursively sort
```

### 18.1.6 Heapsort
**Heapsort** is a comparison-based sorting algorithm that uses a binary heap data structure. It first builds a max-heap from the input data, and then repeatedly extracts the maximum element from the heap and rebuilds the heap.

#### Implementation
```python
def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left
    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]  # Swap
        heapify(arr, n, largest)

def heapsort(arr):
    n = len(arr)

    # Build a max-heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements from the heap
    for i in range(n - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]  # Swap
        heapify(arr, i, 0)  # Heapify the root element
```

### 18.1.7 Radix Sort
**Radix sort** is a non-comparison-based sorting algorithm that sorts numbers by processing individual digits. It works by distributing the numbers into buckets based on their individual digits, starting from the least significant digit to the most significant digit.

#### Implementation
```python
def counting_sort(arr, exp):
    n = len(arr)
    output = [0] * n  # Output array
    count = [0] * 10  # Count array for digits 0-9

    # Count occurrences of each digit
    for i in range(n):
        index = arr[i] // exp
        count[index % 10] += 1

    # Change count[i] so that it contains the actual position of this digit in output[]
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Build the output array
    for i in range(n - 1, -1, -1):
        index = arr[i] // exp
        output[count[index % 10] - 1] = arr[i]
        count[index % 10] -= 1

    # Copy the output array to arr[], so that arr[] now contains sorted numbers
    for i in range(n):
        arr[i] = output[i]

def radix_sort(arr):
    max_num = max(arr)  # Find the maximum number to know the number of digits
    exp = 1  # Exponent for digit place

    while max_num // exp > 0:
        counting_sort(arr, exp)  # Sort by the current digit
        exp *= 10
```

## 18.2 Comparative Analysis of Sorting Algorithms

### 18.2.1 Time Complexity
| Algorithm        | Best Case | Average Case | Worst Case | Space Complexity |
|------------------|-----------|--------------|------------|-------------------|
| Bubble Sort      | O(n)      | O(n^2)       | O(n^2)     | O(1)              |
| Selection Sort   | O(n^2)    | O(n^2)       | O(n^2)     | O(1)              |
| Insertion Sort   | O(n)      | O(n^2)       | O(n^2)     | O(1)              |
| Merge Sort       | O(n log n)| O(n log n)   | O(n log n) | O(n)              |
| Quicksort        | O(n log n)| O(n log n)   | O(n^2)     | O(log n)          |
| Heapsort         | O(n log n)| O(n log n)   | O(n log n) | O(1)              |
| Radix Sort       | O(nk)     | O(nk)        | O(nk)      | O(n + k)          |

**Note**: In the above table, k is the number of digits in the maximum number for radix sort.

### 18.2.2 Space Complexity
- **In-place Sorting**: Algorithms like bubble sort, selection sort, insertion sort, quicksort, and heapsort are in-place, meaning they require a constant amount of additional space (O(1)).
- **Non-in-place Sorting**: Merge sort requires O(n) additional space for the temporary arrays, while radix sort requires O(n + k) space, where k is the range of the input.

### 18.2.3 Stability
- **Stable Sorting Algorithms**: Merge sort and insertion sort are stable, meaning they maintain the relative order of equal elements.
- **Unstable Sorting Algorithms**: Quicksort, heapsort, and selection sort are not stable.

### 18.2.4 Use Cases
- **Bubble Sort**: Simple educational purposes; not suitable for large datasets.
- **Selection Sort**: Useful for small datasets; easy to implement.
- **Insertion Sort**: Efficient for small or nearly sorted datasets.
- **Merge Sort**: Preferred for large datasets and linked lists; stable.
- **Quicksort**: Fastest in practice for average cases; widely used in libraries.
- **Heapsort**: Good for large datasets; not stable but has O(n log n) time complexity.
- **Radix Sort**: Efficient for sorting integers or strings with fixed lengths.

This lesson provided an overview of common sorting algorithms, including their implementations and a comparative analysis based on time and space complexity. Understanding these algorithms is crucial for selecting the appropriate sorting method based on the specific requirements of a problem or application.