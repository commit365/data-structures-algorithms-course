# Lesson 19: Searching Algorithms

Searching algorithms are fundamental techniques used to locate specific elements within a data structure. This lesson will cover the basic searching algorithms, including linear search and binary search, as well as advanced searching techniques such as interpolation search, exponential search, and searching in rotated arrays.

## 19.1 Introduction to Searching Algorithms

### 19.1.1 Linear Search
**Linear search** is the simplest searching algorithm. It sequentially checks each element in the list until the desired element is found or the end of the list is reached. 

#### Characteristics
- **Time Complexity**: O(n), where n is the number of elements in the list.
- **Space Complexity**: O(1), as it requires no additional space.
- **Use Case**: Suitable for small or unsorted lists.

#### Implementation
```python
def linear_search(arr, target):
    for index, value in enumerate(arr):
        if value == target:
            return index  # Return the index of the found element
    return -1  # Return -1 if the element is not found
```

### 19.1.2 Binary Search
**Binary search** is a more efficient algorithm that works on sorted arrays. It repeatedly divides the search interval in half, comparing the target value to the middle element of the array.

#### Characteristics
- **Time Complexity**: O(log n), where n is the number of elements in the list.
- **Space Complexity**: O(1) for iterative implementation, O(log n) for recursive implementation due to call stack.
- **Use Case**: Suitable for large, sorted lists.

#### Implementation
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = left + (right - left) // 2  # Calculate the middle index
        if arr[mid] == target:
            return mid  # Return the index of the found element
        elif arr[mid] < target:
            left = mid + 1  # Search in the right half
        else:
            right = mid - 1  # Search in the left half
    return -1  # Return -1 if the element is not found
```

## 19.2 Advanced Searching Techniques

### 19.2.1 Interpolation Search
**Interpolation search** is an improvement over binary search for uniformly distributed data. It estimates the position of the target value based on the values of the endpoints of the search interval.

#### Characteristics
- **Time Complexity**: O(log log n) on average, O(n) in the worst case.
- **Space Complexity**: O(1).
- **Use Case**: Effective for large, uniformly distributed sorted arrays.

#### Implementation
```python
def interpolation_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high and target >= arr[low] and target <= arr[high]:
        if low == high:
            if arr[low] == target:
                return low
            return -1

        # Estimate the position
        pos = low + ((high - low) // (arr[high] - arr[low]) * (target - arr[low]))

        if arr[pos] == target:
            return pos  # Return the index of the found element
        if arr[pos] < target:
            low = pos + 1  # Search in the right half
        else:
            high = pos - 1  # Search in the left half
    return -1  # Return -1 if the element is not found
```

### 19.2.2 Exponential Search
**Exponential search** is useful for unbounded or infinite lists. It first finds the range where the target may be present and then performs a binary search within that range.

#### Characteristics
- **Time Complexity**: O(log n) for the binary search part, O(log n) for finding the range.
- **Space Complexity**: O(1).
- **Use Case**: Effective for large, unbounded sorted arrays.

#### Implementation
```python
def exponential_search(arr, target):
    if arr[0] == target:
        return 0  # Return if the first element is the target

    index = 1
    while index < len(arr) and arr[index] <= target:
        index *= 2  # Exponentially increase the index

    # Perform binary search in the found range
    return binary_search(arr[:min(index, len(arr))], target)
```

### 19.2.3 Search in Rotated Arrays
Searching in a rotated sorted array involves finding the pivot point where the array was rotated and then performing a binary search in the appropriate half.

#### Characteristics
- **Time Complexity**: O(log n).
- **Space Complexity**: O(1).
- **Use Case**: Useful for searching in arrays that have been rotated (e.g., [4, 5, 6, 7, 0, 1, 2]).

#### Implementation
```python
def search_rotated_array(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            return mid  # Return the index of the found element

        # Determine which side is sorted
        if arr[left] <= arr[mid]:  # Left side is sorted
            if arr[left] <= target < arr[mid]:
                right = mid - 1  # Target is in the left side
            else:
                left = mid + 1  # Target is in the right side
        else:  # Right side is sorted
            if arr[mid] < target <= arr[right]:
                left = mid + 1  # Target is in the right side
            else:
                right = mid - 1  # Target is in the left side

    return -1  # Return -1 if the element is not found
```

## 19.3 Comparative Analysis of Searching Algorithms

### 19.3.1 Time Complexity
| Algorithm              | Best Case | Average Case | Worst Case |
|------------------------|-----------|--------------|------------|
| Linear Search          | O(1)      | O(n)         | O(n)       |
| Binary Search          | O(1)      | O(log n)     | O(log n)   |
| Interpolation Search    | O(1)      | O(log log n) | O(n)       |
| Exponential Search      | O(1)      | O(log n)     | O(log n)   |
| Search in Rotated Array | O(1)      | O(log n)     | O(log n)   |

### 19.3.2 Space Complexity
- **Linear Search**: O(1) - requires no additional space.
- **Binary Search**: O(1) for iterative implementation, O(log n) for recursive implementation.
- **Interpolation Search**: O(1) - requires no additional space.
- **Exponential Search**: O(1) - requires no additional space.
- **Search in Rotated Array**: O(1) - requires no additional space.

### 19.3.3 Use Cases
- **Linear Search**: Simple and effective for small or unsorted datasets.
- **Binary Search**: Efficient for large, sorted datasets.
- **Interpolation Search**: Best for uniformly distributed datasets.
- **Exponential Search**: Suitable for unbounded or infinite lists.
- **Search in Rotated Arrays**: Useful for searching in rotated sorted arrays.

This lesson provided an overview of searching algorithms, including linear search, binary search, and advanced techniques such as interpolation search, exponential search, and searching in rotated arrays. You also learned about their time and space complexities, as well as their practical applications in various scenarios, highlighting their importance in efficiently locating elements within data structures.