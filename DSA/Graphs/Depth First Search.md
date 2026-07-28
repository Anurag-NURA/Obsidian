#DFS for graphs

DFS primally means "**Keep going to the first unvisited neighbour**"

In a **binary tree**, Depth First Search (DFS) starts from the **root node** and explores one branch as deeply as possible before backtracking to explore another branch.

Graphs, however, are different from trees.

- A graph **does not have a predefined root node**.
- A graph can be traversed starting from **any vertex**.
- Therefore, before performing DFS, we first choose a **starting vertex (source vertex)**.

For the traversal, this starting vertex acts as the **first vertex to visit**, and DFS explores the graph by continuously moving to an unvisited neighbour until it cannot proceed any further.

---

## Basic Idea of DFS

Once a starting vertex is chosen:

1. Visit the starting vertex.
2. Move to **one unvisited neighbour**.
3. Repeat this process, always moving to the next unvisited neighbour.
4. If the current vertex has **no unvisited neighbours**, backtrack to the previous vertex.
5. Continue exploring unvisited neighbours from the backtracked vertex.
6. Repeat until every reachable vertex has been visited.

This is why DFS is known as a **depth-wise traversal**.

## Implementation

We will be using recursion to implement **Depth first Search** for our graph. Each recursion will check that the node 