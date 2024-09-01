# Lesson 14: Graphs

## 14.1 Introduction to Graph Data Structures

A **graph** is a collection of nodes (or vertices) and edges that connect pairs of nodes. Graphs are used to model relationships and connections in various applications, such as social networks, transportation systems, and communication networks.

### 14.1.1 Terminology
- **Vertex (Node)**: A fundamental part of a graph that represents an entity (e.g., a person in a social network).
- **Edge**: A connection between two vertices that represents a relationship (e.g., a friendship).
- **Degree**: The number of edges connected to a vertex. In directed graphs, we distinguish between in-degree (incoming edges) and out-degree (outgoing edges).
- **Path**: A sequence of vertices connected by edges.
- **Cycle**: A path that starts and ends at the same vertex without repeating any edges or vertices.
- **Connected Graph**: A graph where there is a path between every pair of vertices.
- **Disconnected Graph**: A graph where at least one pair of vertices does not have a path connecting them.

### 14.1.2 Types of Graphs
- **Directed Graph**: A graph where edges have a direction, indicating a one-way relationship (e.g., Twitter follows).
- **Undirected Graph**: A graph where edges have no direction, indicating a two-way relationship (e.g., Facebook friends).
- **Weighted Graph**: A graph where edges have weights (or costs) associated with them, representing the strength or cost of the connection (e.g., distances between cities).
- **Unweighted Graph**: A graph where all edges are treated equally, without weights.

## 14.2 Representation of Graphs

Graphs can be represented in various ways, with the two most common representations being **adjacency lists** and **adjacency matrices**.

### 14.2.1 Adjacency List
An **adjacency list** is a collection of lists or arrays where each index represents a vertex, and the elements at that index represent the vertices adjacent to it. This representation is efficient in terms of space, especially for sparse graphs.

#### Example of Adjacency List Representation
```python
class Graph:
    def __init__(self):
        self.adjacency_list = {}  # Initialize an empty adjacency list

    def add_vertex(self, vertex):
        if vertex not in self.adjacency_list:
            self.adjacency_list[vertex] = []  # Create an empty list for the new vertex

    def add_edge(self, vertex1, vertex2):
        if vertex1 in self.adjacency_list and vertex2 in self.adjacency_list:
            self.adjacency_list[vertex1].append(vertex2)  # Add an edge from vertex1 to vertex2
            self.adjacency_list[vertex2].append(vertex1)  # Add an edge from vertex2 to vertex1 (for undirected graph)

    def display(self):
        for vertex, edges in self.adjacency_list.items():
            print(f"{vertex}: {', '.join(edges)}")
```

#### Example Usage
```python
graph = Graph()
graph.add_vertex("A")
graph.add_vertex("B")
graph.add_vertex("C")
graph.add_edge("A", "B")
graph.add_edge("A", "C")
graph.add_edge("B", "C")

graph.display()
# Output:
# A: B, C
# B: A, C
# C: A, B
```

### 14.2.2 Adjacency Matrix
An **adjacency matrix** is a 2D array where the rows and columns represent vertices. The element at row i and column j indicates whether there is an edge between vertex i and vertex j. If the graph is weighted, the matrix will contain the weights instead of 1s and 0s.

#### Example of Adjacency Matrix Representation
```python
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.adjacency_matrix = [[0] * num_vertices for _ in range(num_vertices)]  # Initialize a num_vertices x num_vertices matrix

    def add_edge(self, vertex1, vertex2):
        self.adjacency_matrix[vertex1][vertex2] = 1  # Add an edge from vertex1 to vertex2
        self.adjacency_matrix[vertex2][vertex1] = 1  # Add an edge from vertex2 to vertex1 (for undirected graph)

    def display(self):
        for row in self.adjacency_matrix:
            print(' '.join(map(str, row)))
```

#### Example Usage
```python
graph = Graph(3)  # Create a graph with 3 vertices (0, 1, 2)
graph.add_edge(0, 1)
graph.add_edge(0, 2)
graph.add_edge(1, 2)

graph.display()
# Output:
# 0 1 1
# 1 0 1
# 1 1 0
```

## 14.3 Trade-offs Between Representations

### 14.3.1 Adjacency List
**Advantages**:
- More space-efficient for sparse graphs, as it only stores edges that exist.
- Easier to iterate over all edges for a given vertex.

**Disadvantages**:
- Slower to check for the existence of a specific edge, as it requires searching through the list.

### 14.3.2 Adjacency Matrix
**Advantages**:
- Faster to check for the existence of a specific edge (O(1) time complexity).
- Simple to implement and understand.

**Disadvantages**:
- Uses more space, especially for sparse graphs, as it allocates space for all possible edges.
- Inefficient for iterating over edges, as it requires checking all vertices.

## 14.4 Conclusion

This lesson provided an overview of graph data structures, including terminology and types such as directed, undirected, weighted, and unweighted graphs. You learned about the two primary representations of graphs: adjacency lists and adjacency matrices, along with their trade-offs. Understanding these concepts is crucial for effectively working with graphs in various applications, such as network analysis, pathfinding algorithms, and data organization.

[Next: 15. Graph Traversal Algorithms](./15-graph-traversal-algorithms.md)