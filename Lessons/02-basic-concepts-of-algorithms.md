# Lesson 2: Basic Concepts of Algorithms

## 2.1 Definition and Characteristics of Algorithms

### 2.1.1 Definition of an Algorithm
An **algorithm** is a finite set of well-defined instructions or steps designed to perform a specific task or solve a particular problem. Algorithms can be expressed in various forms, including natural language, pseudocode, or programming languages.

### 2.1.2 Characteristics of Algorithms
For an algorithm to be effective, it should possess the following characteristics:

1. **Finiteness**: An algorithm must always terminate after a finite number of steps. It cannot run indefinitely.

2. **Well-Defined Inputs**: An algorithm should have clearly defined inputs, which can be zero or more values.

3. **Well-Defined Outputs**: An algorithm must produce one or more outputs, which are the results of the computations performed.

4. **Effectiveness**: The steps of the algorithm should be basic enough that they can be performed, in principle, by a person using a pencil and paper. Each step should be clear and unambiguous.

5. **Generality**: An algorithm should be applicable to a broad set of problems, not just a specific instance. It should be able to handle different inputs and produce appropriate outputs.

### 2.1.3 Example of an Algorithm
Here’s a simple example of an algorithm to find the maximum number in a list:

**Algorithm: Find Maximum**
1. Start with the first element of the list as the maximum.
2. Compare the maximum with each element in the list:
   - If an element is greater than the current maximum, update the maximum.
3. After checking all elements, return the maximum value.

## 2.2 Introduction to Algorithm Complexity

### 2.2.1 What is Algorithm Complexity?
Algorithm complexity refers to the amount of resources (time and space) that an algorithm consumes as a function of the size of the input. Understanding complexity helps us evaluate the efficiency of an algorithm.

### 2.2.2 Time Complexity
Time complexity measures the amount of time an algorithm takes to complete as a function of the input size. It is often expressed using **Big O notation**, which provides an upper bound on the growth rate of the algorithm's running time.

### 2.2.3 Space Complexity
Space complexity measures the amount of memory space an algorithm uses as a function of the input size. Like time complexity, it is also expressed in Big O notation.

## 2.3 Big O Notation

### 2.3.1 Definition of Big O Notation
**Big O notation** is a mathematical notation used to describe the upper bound of an algorithm's complexity. It provides an approximation of the worst-case scenario for an algorithm's running time or space requirements.

### 2.3.2 Common Big O Notations
Here are some common Big O notations and their meanings:

- **O(1)**: Constant time – The algorithm's running time does not change with the size of the input.
- **O(log n)**: Logarithmic time – The running time grows logarithmically as the input size increases.
- **O(n)**: Linear time – The running time grows linearly with the input size.
- **O(n log n)**: Linearithmic time – The running time grows in proportion to n log n, common in efficient sorting algorithms.
- **O(n^2)**: Quadratic time – The running time grows quadratically with the input size, typical in algorithms with nested loops.
- **O(2^n)**: Exponential time – The running time doubles with each additional input, common in recursive algorithms.

### 2.3.3 Example of Time Complexity
Consider the following Python function that calculates the sum of all elements in a list:

```python
def sum_of_list(lst):
    total = 0
    for num in lst:
        total += num
    return total
```

- **Time Complexity**: O(n) because the algorithm must iterate through each element in the list once.

## 2.4 Growth Rates and Empirical Analysis

### 2.4.1 Growth Rates
Growth rates describe how the running time or space requirements of an algorithm increase as the size of the input increases. Understanding growth rates helps in comparing the efficiency of different algorithms.

### 2.4.2 Empirical Analysis
Empirical analysis involves running algorithms with various input sizes and measuring their actual performance. This analysis can help validate theoretical complexity and provide insights into practical performance.

### 2.4.3 Example of Empirical Analysis
To perform empirical analysis, you can time how long it takes to execute an algorithm with different input sizes:

```python
import time

def example_algorithm(n):
    # Some algorithm with time complexity O(n^2)
    for i in range(n):
        for j in range(n):
            pass  # Simulate some work

# Measure execution time
for size in [100, 200, 300, 400, 500]:
    start_time = time.time()
    example_algorithm(size)
    end_time = time.time()
    print(f"Input size: {size}, Time taken: {end_time - start_time:.6f} seconds")
```

This code will help you observe how the execution time increases with larger input sizes, providing practical insights into the algorithm's performance.

---

In this lesson, you learned the fundamental concepts of algorithms, their characteristics, and the importance of analyzing their complexity. Understanding these concepts will serve as a foundation for the subsequent lessons, where you will explore various data structures and algorithms in more detail.

[Next: 03. Python Basics Refresher](./03-python-basics-refresher.md)