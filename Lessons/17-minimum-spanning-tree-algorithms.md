# Lesson 17: Minimum Spanning Tree Algorithms

Minimum Spanning Tree (MST) algorithms are used to find a subset of edges in a weighted graph that connects all vertices with the minimum total edge weight while avoiding cycles. Two of the most popular algorithms for finding the MST are **Prim's algorithm** and **Kruskal's algorithm**. In this lesson, we will explore these algorithms and their applications in various fields.

## 17.1 Overview of Prim's Algorithm

**Prim's algorithm** is a greedy algorithm that builds the Minimum Spanning Tree by starting from an arbitrary vertex and growing the tree one edge at a time. The algorithm selects the smallest edge that connects a vertex in the tree to a vertex outside the tree.

### 17.1.1 Steps of Prim's Algorithm
1. Initialize a tree with a single vertex (starting point).
2. While the tree does not include all vertices:
   - Find the smallest edge that connects a vertex in the tree to a vertex outside the tree.
   - Add the selected edge and the vertex to the tree.
3. Repeat until all vertices are included.

### 17.1.2 Prim's Algorithm Implementation
Here is an example implementation of Prim's algorithm using a priority queue.

```python
import heapq

class Graph:
    def __init__(self):
        self.adjacency_list = {}  # Initialize an empty adjacency list

    def add_vertex(self, vertex):
        if vertex not in self.adjacency_list:
            self.adjacency_list[vertex] = []  # Create an empty list for the new vertex

    def add_edge(self, vertex1, vertex2, weight):
        self.adjacency_list[vertex1].append((vertex2, weight))  # Add an edge with weight
        self.adjacency_list[vertex2].append((vertex1, weight))  # Add the reverse edge for undirected graph

    def prim(self, start):
        mst = []  # Initialize the Minimum Spanning Tree
        visited = set()  # Keep track of visited vertices
        min_heap = [(0, start)]  # (weight, vertex)

        while min_heap:
            weight, vertex = heapq.heappop(min_heap)  # Get the vertex with the smallest edge
            if vertex not in visited:
                visited.add(vertex)  # Mark the vertex as visited
                mst.append((weight, vertex))  # Add the edge to the MST

                for neighbor, edge_weight in self.adjacency_list[vertex]:
                    if neighbor not in visited:
                        heapq.heappush(min_heap, (edge_weight, neighbor))  # Add unvisited neighbors to the heap

        return mst
```

### 17.1.3 Example Usage
```python
graph = Graph()
graph.add_vertex("A")
graph.add_vertex("B")
graph.add_vertex("C")
graph.add_vertex("D")
graph.add_edge("A", "B", 1)
graph.add_edge("A", "C", 3)
graph.add_edge("B", "C", 1)
graph.add_edge("B", "D", 4)
graph.add_edge("C", "D", 2)

mst = graph.prim("A")
print("Prim's Minimum Spanning Tree:")
for weight, vertex in mst:
    print(f"Vertex: {vertex}, Weight: {weight}")
```

## 17.2 Overview of Kruskal's Algorithm

**Kruskal's algorithm** is another greedy algorithm that finds the Minimum Spanning Tree by considering edges in increasing order of weight. It adds edges to the MST as long as they do not form a cycle.

### 17.2.1 Steps of Kruskal's Algorithm
1. Sort all edges in the graph by weight in non-decreasing order.
2. Initialize an empty tree for the MST.
3. For each edge in the sorted list:
   - If adding the edge does not form a cycle, add it to the MST.
4. Repeat until the MST contains (V - 1) edges, where V is the number of vertices.

### 17.2.2 Kruskal's Algorithm Implementation
Here is an example implementation of Kruskal's algorithm using the Union-Find data structure to detect cycles.

```python
class UnionFind:
    def __init__(self, size):
        self.parent = list(range(size))  # Initialize parent pointers
        self.rank = [0] * size  # Initialize ranks

    def find(self, p):
        if self.parent[p] != p:
            self.parent[p] = self.find(self.parent[p])  # Path compression
        return self.parent[p]

    def union(self, p, q):
        rootP = self.find(p)
        rootQ = self.find(q)
        if rootP != rootQ:
            if self.rank[rootP] > self.rank[rootQ]:
                self.parent[rootQ] = rootP
            elif self.rank[rootP] < self.rank[rootQ]:
                self.parent[rootP] = rootQ
            else:
                self.parent[rootQ] = rootP
                self.rank[rootP] += 1

class Graph:
    def __init__(self):
        self.edges = []  # Initialize an empty list for edges

    def add_edge(self, vertex1, vertex2, weight):
        self.edges.append((weight, vertex1, vertex2))  # Add an edge with weight

    def kruskal(self):
        self.edges.sort()  # Sort edges by weight
        uf = UnionFind(len(self.edges))  # Initialize Union-Find
        mst = []  # Initialize the Minimum Spanning Tree

        for weight, vertex1, vertex2 in self.edges:
            if uf.find(vertex1) != uf.find(vertex2):  # Check if adding edge forms a cycle
                uf.union(vertex1, vertex2)  # Union the two vertices
                mst.append((weight, vertex1, vertex2))  # Add edge to the MST

        return mst
```

### 17.2.3 Example Usage
```python
graph = Graph()
graph.add_edge("A", "B", 1)
graph.add_edge("A", "C", 3)
graph.add_edge("B", "C", 1)
graph.add_edge("B", "D", 4)
graph.add_edge("C", "D", 2)

mst = graph.kruskal()
print("Kruskal's Minimum Spanning Tree:")
for weight, vertex1, vertex2 in mst:
    print(f"Edge: {vertex1} - {vertex2}, Weight: {weight}")
```

## 17.3 Applications of Minimum Spanning Trees

### 17.3.1 Networking
Minimum spanning trees are used in network design to minimize the cost of connecting various nodes. For example, when designing a network of computers, an MST can help determine the least expensive way to lay cables while ensuring all computers are connected.

### 17.3.2 Clustering
In data analysis, MSTs can be used in clustering algorithms to group similar items together. By treating data points as vertices and distances as edges, an MST can help identify clusters based on proximity.

### 17.3.3 Circuit Design
In electrical engineering, MST algorithms are used to design circuits that minimize the total length of wires needed to connect components. This helps reduce costs and improve efficiency in circuit layouts.

### 17.3.4 Urban Planning
Minimum spanning trees can assist in urban planning by optimizing the placement of roads, pipelines, or communication networks to connect various locations with minimal infrastructure costs.

### 17.3.5 Game Development
In game development, MST algorithms can be used to create efficient paths for characters or resources in a game world, ensuring that the environment is navigable with minimal obstacles.

This lesson covered minimum spanning tree algorithms, including Prim's and Kruskal's algorithms, along with their implementations. You also learned about their practical applications in networking, clustering, circuit design, and more, highlighting the importance of MSTs in optimizing connections and minimizing costs across various domains.

[Next: 18. Sorting Algorithms](./18-sorting-algorithms.md)