# Lesson 25: Bit Manipulation

Bit manipulation is a technique that involves directly operating on the binary representations of integers. It is a powerful tool in programming and computer science, allowing for efficient data processing and optimization. This lesson will cover the basics of bitwise operations, their applications, and common problems that can be solved using bit manipulation techniques.

## 25.1 Understanding Bitwise Operations

### 25.1.1 Bitwise Operators
Bitwise operations are performed on the binary representations of integers. The primary bitwise operators include:

- **AND (`&`)**: Compares each bit of two numbers and returns 1 if both bits are 1, otherwise returns 0.
  - Example: `5 & 3` (binary `101 & 011` = `001`, which is 1)
  
- **OR (`|`)**: Compares each bit of two numbers and returns 1 if at least one of the bits is 1.
  - Example: `5 | 3` (binary `101 | 011` = `111`, which is 7)

- **XOR (`^`)**: Compares each bit of two numbers and returns 1 if the bits are different.
  - Example: `5 ^ 3` (binary `101 ^ 011` = `110`, which is 6)

- **NOT (`~`)**: Inverts all the bits of the number.
  - Example: `~5` (binary `~101` = `010`, which is -6 in two's complement)

- **Left Shift (`<<`)**: Shifts the bits of a number to the left, filling in with zeros. This effectively multiplies the number by 2 for each shift.
  - Example: `5 << 1` (binary `101 << 1` = `1010`, which is 10)

- **Right Shift (`>>`)**: Shifts the bits of a number to the right. This effectively divides the number by 2 for each shift.
  - Example: `5 >> 1` (binary `101 >> 1` = `010`, which is 2)

### 25.1.2 Applications of Bitwise Operations
Bitwise operations are used in various applications, including:
- Efficient arithmetic operations.
- Data compression algorithms.
- Cryptography.
- Graphics programming.
- Network programming.

## 25.2 Common Problems and Techniques Using Bit Manipulation

### 25.2.1 Finding Unique Elements
One common problem is finding the unique element in an array where every other element appears twice. This can be efficiently solved using the XOR operator.

#### Implementation
```python
def find_unique(arr):
    unique = 0
    for num in arr:
        unique ^= num  # XOR all elements
    return unique
```

#### Example Usage
```python
arr = [2, 3, 5, 4, 5, 3, 4]
print("Unique element:", find_unique(arr))  # Output: Unique element: 2
```

### 25.2.2 Counting Bits
To count the number of set bits (1s) in the binary representation of a number, you can use bit manipulation.

#### Implementation
```python
def count_set_bits(n):
    count = 0
    while n:
        count += n & 1  # Increment count if the last bit is 1
        n >>= 1  # Right shift to check the next bit
    return count
```

#### Example Usage
```python
n = 29  # Binary representation: 11101
print("Number of set bits:", count_set_bits(n))  # Output: Number of set bits: 4
```

### 25.2.3 Generating Subsets
Bit manipulation can be used to generate all subsets of a set. Each subset can be represented by a binary number where each bit indicates whether an element is included in the subset.

#### Implementation
```python
def generate_subsets(arr):
    n = len(arr)
    subsets = []
    for i in range(1 << n):  # Iterate through all possible combinations
        subset = []
        for j in range(n):
            if i & (1 << j):  # Check if jth element is included
                subset.append(arr[j])
        subsets.append(subset)
    return subsets
```

#### Example Usage
```python
arr = [1, 2, 3]
subsets = generate_subsets(arr)
print("Subsets:")
for subset in subsets:
    print(subset)
# Output: All subsets of [1, 2, 3]
```

### 25.2.4 Swapping Numbers
Bit manipulation can also be used to swap two numbers without using a temporary variable.

#### Implementation
```python
def swap(a, b):
    a ^= b  # Step 1: a now holds the XOR of a and b
    b ^= a  # Step 2: b becomes the original value of a
    a ^= b  # Step 3: a becomes the original value of b
    return a, b
```

#### Example Usage
```python
a, b = 5, 10
print("Before swap:", a, b)
a, b = swap(a, b)
print("After swap:", a, b)  # Output: After swap: 10 5
```

## 25.3 Summary

This lesson provided an overview of bit manipulation, including bitwise operations and their applications. We explored common problems that can be solved using bit manipulation techniques, such as finding unique elements, counting bits, generating subsets, and swapping numbers. Understanding bit manipulation is essential for optimizing algorithms and efficiently handling low-level data operations in programming.