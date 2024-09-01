# Lesson 23: Recursion

Recursion is a fundamental programming technique where a function calls itself to solve smaller instances of the same problem. It is widely used in algorithms and problem-solving due to its elegance and simplicity. This lesson will cover the concept of recursion, its applications, and how to solve problems recursively versus iteratively, including an introduction to tail recursion.

## 23.1 Understanding Recursion

### 23.1.1 Definition
**Recursion** occurs when a function calls itself directly or indirectly to solve a problem. Each recursive call works on a smaller subset of the original problem, and the recursion continues until it reaches a base case, which is a condition that stops the recursion.

### 23.1.2 Components of Recursion
1. **Base Case**: The condition under which the recursive function stops calling itself. It prevents infinite recursion and provides a simple solution for small inputs.
2. **Recursive Case**: The part of the function that includes the recursive call, breaking the problem down into smaller subproblems.

### 23.1.3 Visualizing Recursion
When a recursive function is called, it creates a new stack frame for each call. This stack keeps track of the function's state, including local variables and the point of execution. Once the base case is reached, the function returns values back through the stack, unwinding the calls.

## 23.2 Applications of Recursion

Recursion is commonly used in various algorithms and problem-solving scenarios, including:

### 23.2.1 Factorial Calculation
The factorial of a non-negative integer n (denoted as n!) is the product of all positive integers up to n. It can be defined recursively as:
- Base case: 0! = 1
- Recursive case: n! = n × (n - 1)!

#### Implementation
```python
def factorial(n):
    if n == 0:
        return 1  # Base case
    return n * factorial(n - 1)  # Recursive case
```

### 23.2.2 Fibonacci Sequence
The Fibonacci sequence can be defined recursively as:
- Base cases: F(0) = 0, F(1) = 1
- Recursive case: F(n) = F(n - 1) + F(n - 2)

#### Implementation
```python
def fibonacci(n):
    if n <= 1:
        return n  # Base case
    return fibonacci(n - 1) + fibonacci(n - 2)  # Recursive case
```

### 23.2.3 Tree Traversal
Recursion is particularly useful for traversing tree structures, such as binary trees. In-order, pre-order, and post-order traversals can all be implemented recursively.

#### Example: In-order Traversal
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def in_order_traversal(node):
    if node:
        in_order_traversal(node.left)  # Visit left subtree
        print(node.data, end=' ')  # Visit node
        in_order_traversal(node.right)  # Visit right subtree
```

## 23.3 Solving Problems Recursively vs. Iteratively

### 23.3.1 Recursive Solutions
Recursive solutions can be more intuitive and easier to implement for problems that have a natural recursive structure. However, they may consume more memory due to the call stack and can lead to stack overflow for deep recursions.

### 23.3.2 Iterative Solutions
Iterative solutions use loops to achieve the same result as recursive solutions. They typically use less memory since they do not require additional stack frames.

#### Example: Factorial Iteratively
```python
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result
```

### 23.3.3 Comparison
- **Readability**: Recursive solutions are often more readable and easier to understand.
- **Performance**: Iterative solutions can be more efficient in terms of memory usage.
- **Complexity**: Some problems are more naturally suited to recursion, while others may be easier to solve iteratively.

## 23.4 Tail Recursion

**Tail recursion** is a special case of recursion where the recursive call is the last operation in the function. This allows certain programming languages to optimize the recursive calls, converting them into iterative loops to save stack space.

### 23.4.1 Characteristics of Tail Recursion
- The recursive call must be the final action in the function.
- The function does not need to keep track of previous states, allowing for optimization.

### 23.4.2 Tail Recursive Example
Here’s an example of a tail-recursive function for calculating the factorial:

```python
def tail_recursive_factorial(n, accumulator=1):
    if n == 0:
        return accumulator  # Base case
    return tail_recursive_factorial(n - 1, n * accumulator)  # Tail recursive call
```

### 23.4.3 Tail Recursion Optimization
Not all programming languages support tail call optimization. In languages that do, tail-recursive functions can run in constant stack space, making them as efficient as iterative solutions.

## 23.5 Summary

This lesson provided an overview of recursion, its applications in algorithms, and the comparison between recursive and iterative solutions. We also explored the concept of tail recursion and its benefits. Understanding recursion is essential for solving complex problems and implementing algorithms effectively in programming.

[Next: 24. Backtracking Algorithms](./24-backtracking-algorithms.md)