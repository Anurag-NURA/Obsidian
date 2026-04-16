### 1. Edge List
![[Pasted image 20250524220710.png]]

The total *Space Consumed* in this Vertex list is the number of rows consumed i.e., $O(|V|)$, where $|V|$ is number of elements in set V. 

 For the edge list, we are storing characters in the first two fields of `Edge` object/structure. But we are NOT storing the actual character instead we are storing their address i.e., references or pointers to the name in the vertex list.
 Each row will consume same memory.
$$\therefore total \space space \space consumed = O(|V| + |E|)$$

- `How much time will we take to find all nodes Adjacent to a given node ?`
Answer: $O(|E|)$, As we have to scan the whole *Edge list*. We will have to perform a `linear search` to go though all the entries in the list and to see if the start or end node in the entry is our given node.

- `How much time will we take to find if two given nodes are Connected?`
Answer: For connected nodes we will be perform a linear search on *Edge List*. Worst case: $O(|E|)$. 

- `How costly is this O(|E|) ?`
Answer: If we remember from [[Intro]], we discussed that number of edges in an undirected graph is $0<|E|<n(n-1)$ and for directed graph it will be $0<|E|< \frac{n(n-1)}{2}$. From the equation we can also write $O(|E|)$ = $O(|V|*|V|)$, which is costly.

Example:
![[Pasted image 20250524215255.png]]

### 2. Adjacency Matrix
### 3. Adjacency List