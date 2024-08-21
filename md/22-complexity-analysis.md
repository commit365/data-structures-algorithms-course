# Lesson 22: Complexity Analysis

Complexity analysis is a crucial aspect of algorithm design and evaluation. It helps in understanding the efficiency of algorithms in terms of time and space requirements. This lesson will provide a deep dive into time and space complexity analysis, including best, worst, and average case scenarios, as well as amortized and probabilistic analysis.

## 22.1 Time Complexity Analysis

### 22.1.1 Definition
**Time complexity** measures the amount of time an algorithm takes to complete as a function of the length of the input. It provides an upper bound on the running time, allowing developers to compare the efficiency of different algorithms.

### 22.1.2 Big O Notation
Time complexity is often expressed using **Big O notation**, which describes the upper bound of an algorithm's growth rate. Common time complexities include:
- **O(1)**: Constant time – the algorithm takes the same amount of time regardless of input size.
- **O(log n)**: Logarithmic time – the time grows logarithmically as the input size increases.
- **O(n)**: Linear time – the time grows linearly with the input size.
- **O(n log n)**: Linearithmic time – common in efficient sorting algorithms.
- **O(n²)**: Quadratic time – the time grows quadratically with the input size, typical in algorithms with nested loops.
- **O(2^n)**: Exponential time – the time doubles with each additional input element, common in recursive algorithms.

### 22.1.3 Best, Worst, and Average Case Scenarios
- **Best Case**: The minimum time taken by an algorithm for a specific input size. It represents the scenario where the algorithm performs the least number of operations.
- **Worst Case**: The maximum time taken by an algorithm for a specific input size. It represents the scenario where the algorithm performs the most operations, providing an upper bound on performance.
- **Average Case**: The expected time taken by an algorithm over all possible inputs of a specific size. It is often more complex to calculate and requires knowledge of the distribution of inputs.

### 22.1.4 Amortized Analysis
**Amortized analysis** provides a way to analyze the average time complexity of an operation over a sequence of operations, rather than on a single operation. This type of analysis is useful when an operation may take a long time occasionally but is generally fast.

#### Example: Dynamic Array
When adding elements to a dynamic array, the average time complexity for appending an element is O(1). However, occasionally, the array needs to be resized, which takes O(n) time. Amortized analysis shows that the average time per operation remains O(1) over a series of insertions.

## 22.2 Space Complexity Analysis

### 22.2.1 Definition
**Space complexity** measures the amount of memory an algorithm uses relative to the input size. It includes both the space required for the input and any additional space used by the algorithm.

### 22.2.2 Components of Space Complexity
- **Fixed Part**: The space required for constants, simple variables, fixed-size variables, and program code. This part does not depend on the size of the input.
- **Variable Part**: The space required for dynamic memory allocation, recursion stack space, and other variable-size data structures. This part depends on the size of the input.

### 22.2.3 Big O Notation for Space Complexity
Similar to time complexity, space complexity is also expressed using Big O notation. For example:
- **O(1)**: Constant space – the algorithm uses a fixed amount of space.
- **O(n)**: Linear space – the space grows linearly with the input size.
- **O(n²)**: Quadratic space – the space grows quadratically with the input size.

## 22.3 Probabilistic Analysis

**Probabilistic analysis** evaluates the expected performance of an algorithm based on the probability of different inputs. This type of analysis is particularly useful for algorithms that rely on randomization or when the input distribution is not uniform.

### 22.3.1 Randomized Algorithms
Randomized algorithms use random numbers to influence their behavior. They can provide better average-case performance than deterministic algorithms. For example, randomized quicksort can achieve O(n log n) expected time complexity.

### 22.3.2 Expected Time Complexity
The expected time complexity is calculated based on the likelihood of different outcomes. For example, if an algorithm has a 50% chance of taking O(n) time and a 50% chance of taking O(1) time, the expected time complexity can be calculated as:
$$
E[T] = 0.5 \cdot O(n) + 0.5 \cdot O(1) = O(n)
$$

## 22.4 Summary

This lesson provided a comprehensive overview of complexity analysis, focusing on time and space complexity. We explored best, worst, and average case scenarios, as well as amortized and probabilistic analysis. Understanding these concepts is crucial for evaluating algorithm efficiency and making informed decisions in algorithm design and implementation.