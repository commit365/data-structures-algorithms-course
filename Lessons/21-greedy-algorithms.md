# Lesson 21: Greedy Algorithms

Greedy algorithms are a class of algorithms that make locally optimal choices at each step with the hope of finding a global optimum. This approach is often used in optimization problems where a solution can be built incrementally.

## 21.1 Understanding the Greedy Algorithm Paradigm

### 21.1.1 Principles of Greedy Algorithms
Greedy algorithms operate based on the following principles:
- **Local Optimal Choice**: At each step, the algorithm selects the best option available without considering the overall problem. This choice is made based on some criteria that appear to be the best at that moment.
- **Feasibility**: The chosen option must satisfy the problem's constraints.
- **Irrevocability**: Once a choice is made, it cannot be undone. The algorithm does not backtrack to reconsider previous choices.

### 21.1.2 When to Use Greedy Algorithms
Greedy algorithms are suitable for problems that exhibit the following properties:
- **Optimal Substructure**: The optimal solution to the problem can be constructed from optimal solutions to its subproblems.
- **Greedy Choice Property**: A global optimum can be reached by selecting a local optimum.

## 21.2 Examples and Applications of Greedy Algorithms

### 21.2.1 Coin Change Problem
The **coin change problem** involves finding the minimum number of coins needed to make a certain amount of money using a given set of denominations. A greedy approach works well when the coin denominations are canonical (e.g., U.S. coins).

#### Implementation
```python
def coin_change(coins, amount):
    coins.sort(reverse=True)  # Sort coins in descending order
    count = 0
    for coin in coins:
        while amount >= coin:
            amount -= coin  # Subtract coin value from amount
            count += 1  # Increment coin count
    return count if amount == 0 else -1  # Return count or -1 if change cannot be made
```

#### Example Usage
```python
coins = [1, 5, 10, 25]  # Coin denominations
amount = 63
print("Minimum coins needed:", coin_change(coins, amount))  # Output: 6 (2 quarters, 1 dime, 1 nickel, 3 pennies)
```

### 21.2.2 Activity Selection Problem
The **activity selection problem** involves selecting the maximum number of activities that do not overlap, given their start and finish times. The greedy strategy is to always select the activity that finishes first.

#### Implementation
```python
def activity_selection(activities):
    # Sort activities based on finish time
    activities.sort(key=lambda x: x[1])
    selected_activities = [activities[0]]  # Select the first activity

    last_finish_time = activities[0][1]
    for i in range(1, len(activities)):
        if activities[i][0] >= last_finish_time:  # If the activity starts after the last selected one finishes
            selected_activities.append(activities[i])
            last_finish_time = activities[i][1]  # Update the last finish time

    return selected_activities
```

#### Example Usage
```python
activities = [(0, 6), (1, 4), (3, 5), (4, 7), (5, 9), (8, 9)]
selected = activity_selection(activities)
print("Selected activities:", selected)  # Output: Selected activities: [(0, 6), (6, 9)]
```

### 21.2.3 Huffman Coding
**Huffman coding** is a greedy algorithm used for data compression. It assigns variable-length codes to input characters based on their frequencies, with more frequent characters receiving shorter codes.

#### Steps of Huffman Coding
1. Count the frequency of each character in the input.
2. Build a priority queue (min-heap) of nodes, where each node represents a character and its frequency.
3. While there is more than one node in the queue:
   - Remove the two nodes with the lowest frequencies.
   - Create a new internal node with these two nodes as children and with a frequency equal to the sum of their frequencies.
   - Insert the new node back into the priority queue.
4. The remaining node is the root of the Huffman tree, and codes can be generated by traversing the tree.

#### Implementation
```python
import heapq
from collections import defaultdict

class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq  # Comparison based on frequency

def huffman_coding(char_freq):
    # Create a priority queue (min-heap)
    priority_queue = [Node(char, freq) for char, freq in char_freq.items()]
    heapq.heapify(priority_queue)

    while len(priority_queue) > 1:
        left = heapq.heappop(priority_queue)  # Get the two nodes with the lowest frequency
        right = heapq.heappop(priority_queue)
        merged = Node(None, left.freq + right.freq)  # Create a new internal node
        merged.left = left
        merged.right = right
        heapq.heappush(priority_queue, merged)  # Push the new node back into the queue

    # Generate codes from the Huffman tree
    root = priority_queue[0]
    codes = {}

    def generate_codes(node, current_code):
        if node is not None:
            if node.char is not None:  # Leaf node
                codes[node.char] = current_code
            generate_codes(node.left, current_code + "0")  # Traverse left
            generate_codes(node.right, current_code + "1")  # Traverse right

    generate_codes(root, "")
    return codes
```

#### Example Usage
```python
char_freq = {'a': 5, 'b': 9, 'c': 12, 'd': 13, 'e': 16, 'f': 45}
huffman_codes = huffman_coding(char_freq)
print("Huffman Codes:", huffman_codes)
```

## 21.3 Applications of Greedy Algorithms

### 21.3.1 Networking
Greedy algorithms are used in network routing protocols to find optimal paths for data transmission, minimizing latency and maximizing bandwidth.

### 21.3.2 Clustering
In clustering algorithms, greedy methods can efficiently group similar items together based on proximity or similarity metrics.

### 21.3.3 Resource Allocation
Greedy algorithms can be applied to resource allocation problems, such as scheduling tasks or assigning resources to maximize efficiency.

### 21.3.4 Data Compression
Huffman coding, a greedy algorithm, is widely used in data compression techniques to reduce file sizes while preserving information.

### 21.3.5 Game Development
Greedy algorithms can be used in game development for AI decision-making, where characters make the best immediate choice based on available options.

This lesson provided an overview of the greedy algorithm paradigm, including its principles, examples, and applications. You learned about classic problems such as the coin change problem, activity selection, and Huffman coding, demonstrating the effectiveness of greedy algorithms in solving optimization problems efficiently.

[Next: 22. Complexity Analysis](./22-complexity-analysis.md)