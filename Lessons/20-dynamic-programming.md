# Lesson 20: Dynamic Programming

Dynamic programming (DP) is a powerful algorithmic technique used to solve complex problems by breaking them down into simpler subproblems. It is particularly effective for optimization problems and is characterized by overlapping subproblems and optimal substructure properties.

## 20.1 Introduction to Dynamic Programming Concepts

### 20.1.1 Key Concepts
- **Overlapping Subproblems**: In dynamic programming, the problem can be broken down into smaller subproblems that are solved independently. However, the same subproblems are solved multiple times, making it inefficient if solved naively.
  
- **Optimal Substructure**: A problem exhibits optimal substructure if an optimal solution to the problem can be constructed from optimal solutions to its subproblems. This property allows us to build solutions incrementally.

### 20.1.2 Approaches to Dynamic Programming
Dynamic programming can be implemented using two main approaches:
- **Top-Down Approach (Memoization)**: This approach involves solving the problem recursively and storing the results of subproblems in a table (or array) to avoid redundant calculations.
  
- **Bottom-Up Approach (Tabulation)**: This approach involves solving the problem iteratively by filling up a table based on previously computed values, starting from the smallest subproblems and building up to the original problem.

## 20.2 Solving Classic Problems Using Dynamic Programming

### 20.2.1 Fibonacci Sequence
The Fibonacci sequence is a classic example of a problem that can be solved using dynamic programming. The nth Fibonacci number is defined as:
- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2) for n > 1

#### Implementation Using Memoization
```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]  # Return cached value
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n - 1, memo) + fibonacci_memo(n - 2, memo)  # Cache the result
    return memo[n]
```

#### Implementation Using Tabulation
```python
def fibonacci_tab(n):
    if n <= 1:
        return n
    fib = [0] * (n + 1)
    fib[1] = 1
    for i in range(2, n + 1):
        fib[i] = fib[i - 1] + fib[i - 2]  # Build the table
    return fib[n]
```

### 20.2.2 Knapsack Problem
The **0/1 Knapsack problem** is a classic optimization problem where you have a knapsack with a maximum weight capacity and a set of items, each with a weight and a value. The goal is to maximize the total value in the knapsack without exceeding the weight capacity.

#### Implementation Using Dynamic Programming
```python
def knapsack(weights, values, capacity):
    n = len(values)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]  # Create a DP table

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i - 1] <= w:
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])  # Include or exclude the item
            else:
                dp[i][w] = dp[i - 1][w]  # Exclude the item

    return dp[n][capacity]  # Maximum value
```

### 20.2.3 Longest Common Subsequence (LCS)
The **Longest Common Subsequence** problem involves finding the longest subsequence common to two sequences. It is a classic problem in string processing.

#### Implementation Using Dynamic Programming
```python
def lcs(X, Y):
    m, n = len(X), len(Y)
    dp = [[0] * (n + 1) for _ in range(m + 1)]  # Create a DP table

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if X[i - 1] == Y[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1  # Characters match
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])  # Take the maximum

    return dp[m][n]  # Length of LCS
```

### 20.2.4 Matrix Chain Multiplication
The **Matrix Chain Multiplication** problem involves determining the most efficient way to multiply a given sequence of matrices. The goal is to minimize the number of scalar multiplications needed.

#### Implementation Using Dynamic Programming
```python
def matrix_chain_order(p):
    n = len(p) - 1  # Number of matrices
    dp = [[0] * n for _ in range(n)]  # Create a DP table

    for length in range(2, n + 1):  # Length of the chain
        for i in range(n - length + 1):
            j = i + length - 1
            dp[i][j] = float('inf')  # Initialize to infinity
            for k in range(i, j):
                # Calculate cost
                cost = dp[i][k] + dp[k + 1][j] + p[i] * p[k + 1] * p[j + 1]
                dp[i][j] = min(dp[i][j], cost)  # Update minimum cost

    return dp[0][n - 1]  # Minimum cost
```

## 20.3 Summary

Dynamic programming is a powerful technique used to solve optimization problems by breaking them down into simpler subproblems. In this lesson, we explored several classic problems, including the Fibonacci sequence, the 0/1 Knapsack problem, the Longest Common Subsequence, and Matrix Chain Multiplication. Each problem was solved using dynamic programming techniques, demonstrating the efficiency and effectiveness of this approach in algorithm design. Understanding dynamic programming is crucial for tackling complex problems in computer science and software development.

[Next: 21. Greedy Algorithms](./21-greedy-algorithms.md)