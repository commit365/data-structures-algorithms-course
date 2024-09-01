# Lesson 16: Shortest Path Algorithms

Shortest path algorithms are essential for finding the most efficient route between nodes in a graph. These algorithms are widely used in various applications, including GPS navigation, network routing, and game development. In this lesson, we will cover three fundamental shortest path algorithms: **Dijkstra's algorithm**, **Bellman-Ford algorithm**, and **Floyd-Warshall algorithm**.

## 16.1 Introduction to Shortest Path Algorithms

### 16.1.1 Dijkstra's Algorithm
**Dijkstra's algorithm** is a greedy algorithm used to find the shortest path from a source vertex to all other vertices in a weighted graph with non-negative edge weights. It maintains a set of visited nodes and continuously expands the shortest path to the nearest unvisited node.

#### Steps of Dijkstra's Algorithm
1. Initialize distances from the source to all vertices as infinite, except for the source itself, which is set to 0.
2. Use a priority queue to select the vertex with the smallest distance.
3. For the selected vertex, update the distances to its adjacent vertices.
4. Mark the selected vertex as visited and repeat until all vertices have been processed.

#### Dijkstra's Algorithm Implementation
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

    def dijkstra(self, start):
        # Initialize distances and priority queue
        distances = {vertex: float('infinity') for vertex in self.adjacency_list}
        distances[start] = 0
        priority_queue = [(0, start)]  # (distance, vertex)

        while priority_queue:
            current_distance, current_vertex = heapq.heappop(priority_queue)

            # Nodes can be added multiple times to the priority queue
            if current_distance > distances[current_vertex]:
                continue

            for neighbor, weight in self.adjacency_list[current_vertex]:
                distance = current_distance + weight

                # Only consider this new path if it's better
                if distance < distances[neighbor]:
                    distances[neighbor] = distance
                    heapq.heappush(priority_queue, (distance, neighbor))

        return distances
```

### 16.1.2 Bellman-Ford Algorithm
The **Bellman-Ford algorithm** is another shortest path algorithm that can handle graphs with negative edge weights. Unlike Dijkstra's algorithm, it can also detect negative weight cycles.

#### Steps of Bellman-Ford Algorithm
1. Initialize distances from the source to all vertices as infinite, except for the source itself, which is set to 0.
2. Relax all edges up to (V - 1) times, where V is the number of vertices. This means that for each edge, if the distance to the destination vertex can be shortened by taking the edge, update the distance.
3. Check for negative weight cycles by iterating through all edges again. If a distance can still be updated, a negative cycle exists.

#### Bellman-Ford Algorithm Implementation
```python
class Graph:
    def __init__(self):
        self.edges = []  # Initialize an empty list for edges

    def add_edge(self, vertex1, vertex2, weight):
        self.edges.append((vertex1, vertex2, weight))  # Add an edge with weight

    def bellman_ford(self, start):
        distances = {vertex: float('infinity') for vertex in set([v for edge in self.edges for v in edge[:2]])}
        distances[start] = 0

        for _ in range(len(distances) - 1):
            for vertex1, vertex2, weight in self.edges:
                if distances[vertex1] + weight < distances[vertex2]:
                    distances[vertex2] = distances[vertex1] + weight

        # Check for negative weight cycles
        for vertex1, vertex2, weight in self.edges:
            if distances[vertex1] + weight < distances[vertex2]:
                raise Exception("Graph contains a negative weight cycle")

        return distances
```

### 16.1.3 Floyd-Warshall Algorithm
The **Floyd-Warshall algorithm** is a dynamic programming algorithm used to find the shortest paths between all pairs of vertices in a weighted graph. It can handle negative weights but not negative weight cycles.

#### Steps of Floyd-Warshall Algorithm
1. Create a distance matrix initialized with the weights of the edges. If there is no edge between two vertices, set the distance to infinity.
2. For each vertex k, update the distance between every pair of vertices (i, j) by checking if the path from i to j through k is shorter than the current known distance.

#### Floyd-Warshall Algorithm Implementation
```python
def floyd_warshall(vertices, edges):
    # Initialize distance matrix
    distance = [[float('inf')] * len(vertices) for _ in range(len(vertices))]
    for i in range(len(vertices)):
        distance[i][i] = 0  # Distance to self is zero

    for vertex1, vertex2, weight in edges:
        distance[vertex1][vertex2] = weight  # Set initial distances

    # Update distances based on intermediate vertices
    for k in range(len(vertices)):
        for i in range(len(vertices)):
            for j in range(len(vertices)):
                if distance[i][j] > distance[i][k] + distance[k][j]:
                    distance[i][j] = distance[i][k] + distance[k][j]

    return distance
```

## 16.2 Practical Applications

### 16.2.1 GPS Navigation
Shortest path algorithms, particularly Dijkstra's algorithm, are widely used in GPS navigation systems to find the quickest route between two locations on a map. The road network can be represented as a graph, with intersections as vertices and roads as edges.

### 16.2.2 Network Routing
In computer networks, shortest path algorithms help determine the most efficient route for data packets to travel from one node to another. Algorithms like Dijkstra's and Bellman-Ford are used in routing protocols to optimize data transmission.

### 16.2.3 Game Development
Shortest path algorithms are essential in game development for AI pathfinding. They help characters navigate through complex environments, find the shortest route to objectives, and avoid obstacles.

### 16.2.4 Urban Planning
In urban planning, shortest path algorithms can assist in designing efficient transportation systems by analyzing traffic patterns and optimizing routes for public transport.

### 16.2.5 Robotics
In robotics, shortest path algorithms are used for navigation and movement planning, allowing robots to find optimal paths in dynamic environments while avoiding obstacles.

This lesson provided an introduction to shortest path algorithms, including Dijkstra's, Bellman-Ford, and Floyd-Warshall algorithms. You learned about their implementations and practical applications in GPS navigation, network routing, and game development, highlighting their importance in efficiently finding paths in various scenarios.

[Next: 17. Minimum Spanning Tree Algorithms](./17-minimum-spanning-tree-algorithms.md)