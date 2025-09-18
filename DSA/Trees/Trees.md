It can be defined as a collection of entities called nodes linked together to simulate a Hierarchy.
It is a non linear data structure.
The topmost node in the tree is called _Root of the tree_.


![[Pasted image 20250309085039.png]]

Root Node: Top Most node of the tree (It is the only link without any parent)

Nodes: They are linked together to form a hierarchy.

Link: Shows a link between two nodes.

Children: 2 and 3 node will be called the children of 1, or 1 will be called parent of 2 and 3

Siblings: Children of same parents are called siblings. 2 and 3 are siblings because they have a same parent i.e., 1.
![[Pasted image 20250309085817.png]]

Leaf Node: Node without any child will be called leaf node.![[Pasted image 20250309085645.png]]

Internal Node: All other nodes with at least one child will be called internal nodes.

Now, if we go from any point A to point B then A is Ancestor of B or B will be called descendant of A. 1,2 and 5 are ancestors of 10 and 10 is descendant of 1,2 and 5 
![[Pasted image 20250309090357.png]]


### Trees are Recursive data structure:
Each subtree of a tree is itself a tree. This self-similar structure makes recursion a natural and powerful approach when working with trees.
![[Pasted image 20250309090614.png]]

The most common way of implementing Trees is dynamically created nodes linked using Pointers.
If there are N nodes in a tree then there will be N-1 edges.
### Depths and Height:

![[Pasted image 20250309093443.png]]
from Root node of tree:
Depth of node 5 is 2,
Depth of nodes 2 and 3 is 1,
Depth of nodes 4, 5, 6, 7 and 8  is 2,
Depth of nodes 9, 10 and 11 is  3


![[Pasted image 20250309094826.png]]Height of longest path of a leaf from 3 is 2 (towards leaf node 11)
Height of leaf nodes will be zero.

### Applications:
![[Pasted image 20250309101127.png]]
### **Types of Trees**

- [[Binary Tree]]: Each node has at most two children, called left and right child.
![[Pasted image 20250309101001.png]]
- **Binary Search Tree (BST)**: A binary tree where the left child contains values less than the parent, and the right child contains values greater.
- **AVL Tree**: A balanced BST where the height difference between left and right subtrees is at most 1.
- **Heap Tree**: A special tree used for heap-related operations (e.g., min-heaps and max-heaps).
- **Trie**: A tree structure used for storing strings, commonly for dictionaries.

