#BFS for graphs

BFS primally means "**Travel to immediate neighbor first**"

In a **binary tree**, Breadth First Search (BFS) starts from the **root node** and explores the tree **level by level**, visiting all nodes at the current level before moving to the next.

Graphs, however, are different from trees.

- A graph **does not have a predefined root node**.
- A graph can be traversed starting from **any vertex**.
- Therefore, before performing BFS, we first choose a **starting vertex (source vertex)**.

For the traversal, this starting vertex acts as the **first vertex to visit**, and BFS explores the graph outward from this point.

## Basic Idea of BFS

Once a starting vertex is chosen:

1. Visit the starting vertex.
2. Visit all of its **immediate neighbours**.
3. After all neighbours at the current level have been visited, move to the neighbours of those vertices.
4. Continue this process until there are no more reachable vertices to visit.

This is why BFS is known as a **level-wise traversal**.

```cpp
#include <iostream>
#include <list>
#include <queue>
#include <vector>

using namespace std;

class Graph {
  int vertices;
  list<int> *adjList;

public:
  Graph(int v) {
    this->vertices = v;
    adjList = new list<int>[vertices];
  }

  void addEdge(int u, int v) {
    adjList[u].push_back(v);
    adjList[v].push_back(u);
  }

  void bfs() {
    queue<int> Q;
    vector<bool> visited(vertices, false);

    // we pushed source node into the queue first
    Q.push(0);
    visited[0] = true;

    while (!Q.empty()) {
      int u = Q.front();
      Q.pop();

      cout << u << " ";
      for (int v : adjList[u]) {
        // v --> immediate neighbour
        if (!visited[v]) {
          visited[v] = true;
          Q.push(v);
        }
      }
      cout << endl;
    }
  }
};

int main() {

  Graph g(5);

  g.addEdge(1, 3);
  g.addEdge(1, 0);
  g.addEdge(1, 2);
  g.addEdge(2, 3);
  g.addEdge(2, 4);

  g.bfs();
  return 0;
}

```