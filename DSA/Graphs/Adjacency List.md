## What is an #Adjacency-List?

An **Adjacency List** is a graph representation where every vertex stores a list of all vertices directly connected to it.

Instead of storing all possible connections (like an adjacency matrix), we only store the **existing edges**, making it much more memory efficient for sparse graphs.

### C++ Representation

```
list<int>* adjList;
```

or more commonly in modern C++:

```
vector<vector<int>> adjList;
```

Each index represents a vertex.

Example:

```
adjList[0] -> {1, 4}
adjList[1] -> {0, 2, 3}
adjList[2] -> {1}
...
```

---
### What about `new list<int>[vertices]`?

Suppose

```cpp
vertices = 5;
```

and we write

```cpp
adjList = new std::list<int>[vertices];
```

This is completely different.

The compiler allocates **five separate list objects**.

```
Stack

adjList
+-------+
| 0x700 |
+-------+

            Heap

0x700
+--------+--------+--------+--------+--------+
| list 0 | list 1 | list 2 | list 3 | list 4 |
+--------+--------+--------+--------+--------+
```

Each one starts empty.

Notice something important:

These are **not nodes of a linked list**.

They are simply **five independent `std::list` objects stored consecutively**.

Each object will later manage its own linked list.

### Why is `adjList[2]` valid?

Because arrays and pointers are closely related.

This learning block shows the relationship between array indexing and pointer arithmetic:

![[Pasted image 20260723130419.png]]

![[Pasted image 20260723130429.png]]

![[Pasted image 20260723130440.png]]

# Undirected Graph

In an **undirected graph**, an edge works in **both directions**.

If

``` 
u -- v
```

exists,

then

```
u can reach v
v can reach u
```

Therefore, while inserting an edge, we must insert it into **both adjacency lists**.

## Code

```
void addEdge(int u, int v) {

    // u ---- v
    adjList[u].push_back(v);

    // v ---- u
    adjList[v].push_back(u);
}
```

### Key Observation

Every edge is stored **twice**.

Example:

```
Edge : 2 --- 5
```

Stored as

```
adjList[2] -> 5
adjList[5] -> 2
```

---

## Example

### Graph

### Adjacency List

```
0 → 1

1 → 0, 2, 3

2 → 1, 3, 4

3 → 1, 2

4 → 2
```

---

# Directed Graph

A directed graph has **one-way edges**.

```
u ----> v
```

means

```
u can reach v

v cannot reach u
```

unless another edge

```
v ----> u
```

also exists.

---

## Code

```
void addEdge(int u, int v) {

    // Only one direction
    adjList[u].push_back(v);
}
```

Notice that we **do not** insert

```
adjList[v].push_back(u);
```

because the graph is directional.

---

## Example

### Graph

### Adjacency List

```
0 → 1

1 → 2, 3

2 → 3, 4

3 →

4 →
```

Observe that:

```
0 → 1
```

does **not** imply

```
1 → 0
```

---

# Complete Example (Undirected)

```cpp
#include <iostream>
#include <list>
using namespace std;

class Graph {
    int vertices;
    list<int>* adjList;

public:
    Graph(int v) {
        vertices = v;
        adjList = new list<int>[vertices];
    }

    void addEdge(int u, int v) {

        // Since this is an UNDIRECTED graph,
        // store the edge in both adjacency lists.

        adjList[u].push_back(v);
        adjList[v].push_back(u);
    }

    void printAdjList() {

        for (int i = 0; i < vertices; i++) {

            cout << i << " : ";

            for (int neighbour : adjList[i])
                cout << neighbour << " ";

            cout << endl;
        }
    }
};

int main() {

    Graph g(5);

    g.addEdge(1,3);
    g.addEdge(1,0);
    g.addEdge(1,2);
    g.addEdge(2,3);
    g.addEdge(2,4);

    g.printAdjList();
}
```

---

# Time Complexity

|Operation|Complexity|
|---|---|
|Add Edge|**O(1)**|
|Print Graph|**O(V + E)**|
|DFS|**O(V + E)**|
|BFS|**O(V + E)**|
|Check all neighbours of one vertex|**O(degree of vertex)**|

---

# Space Complexity

For **V vertices** and **E edges**:

### Undirected Graph

```
O(V + 2E)
```

Since every edge is stored twice.

---

### Directed Graph

```
O(V + E)
```

Since every edge is stored only once.

---

# Why is an Adjacency List Preferred?

Compared to an adjacency matrix:

- Uses memory only for **existing edges**.
- Ideal for **sparse graphs** where the number of edges is much smaller than V2V^2V2.
- BFS and DFS naturally iterate over neighbours using adjacency lists.

---

# Key Points to Remember

- Each index in the adjacency list represents a **vertex**.
- The list at that index stores all **adjacent (neighbouring) vertices**.
- **Undirected graph:** insert both `u → v` and `v → u`.
- **Directed graph:** insert only `u → v`.
- Every undirected edge appears **twice** in memory.
- Every directed edge appears **once**.
- Traversing all neighbours of a vertex takes **O(degree(vertex))**.
- Adjacency lists are the standard graph representation used with **BFS**, **DFS**, **Topological Sort**, **Dijkstra's Algorithm**, **Prim's Algorithm**, and most other graph algorithms because they are efficient for sparse graphs.
