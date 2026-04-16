![[Pasted image 20250309101607.png]]

### What is a Binary Tree ?
A **binary tree** is a type of tree data structure where:
- Each node has at most **two children**.
- These children are referred to as the **left child** and **right child**.

If a tree has just one node, then also its a binary tree. The only condition for a binary tree is that, __Node cannot have more than two children__.

### Strict Binary Tree
![[Pasted image 20250509213049.png]]
### Complete Binary Tree
![[Pasted image 20250309102730.png]]

A complete binary tree is a binary tree where every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. This means that all internal nodes have two children, and the leaf nodes are filled from left to right

__Internal Node:__ In a **binary tree**, an **internal node** is any node that **has at least one child**—meaning it is not a leaf node.

Key characteristics of internal nodes:
- They **exist between the root and the leaves**.
- They **must have at least one child** (left, right, or both).
- They **help form the structure** of the tree.

In the following binary tree:
	A 
	/\
	B  C 
	/\ 
	D E

- **Internal nodes**: `A`, `B` (since they have children).
- **Leaf nodes**: `C`, `D`, `E` (since they have no children).

### Structure of a Binary Tree
 ![[Pasted image 20250309101001.png]]
 A binary tree is made up of nodes, starting with a **root node**.  
- Each node contains:
- **Data**: The value stored in the node.    
-  **Left Pointer**: Points to the left child (or is null if there’s no left child).    
- **Right Pointer**: Points to the right child (or is null if there’s no right child).

```C
typedef struct BstNode {
  int data;
  struct BstNode* left;
  struct BstNode* right;
} BstNode;

BstNode* GetNewNode(int data){
  BstNode* newNode = (BstNode*)malloc(sizeof(BstNode));
  newNode->data = data;
  newNode->left = newNode->right = NULL;
  return newNode;
}
```
### Levels in Binary Tree
![[Pasted image 20250309121004.png]]

![[Pasted image 20250310210409.png]]

 Then height of the tree can be calculated through the above equation:
 n = $2^{n+1}$ -1 
 $2^{n+1}$ = (n+1)
 h = $log_2$ (n+1) -1

From above Binary Tree, number of nodes is 15.
$\therefore$ (n+1) = (15+1) = $log_2 16$ -1 = 4 -1 = 3

Height of complete binary tree =  $log_2 n$ = $log_2 15$ = 3.9068 = 3 (after taking integral part)

### Insertion of a Node in a Binary Tree

```C
BstNode* insert(BstNode* root, int data){
	if(root == NULL){
		//if tree is empty
		root = GetNewNode(data); 
	}else if(data <= root ->data){
		root -> left = insert(root->left, data);
	}else {
		root-> right = insert(root->right, data);
	}
	return root;
}
```
### Height of a Node
![[Pasted image 20250511214237.png]]

`Implementation of Height of a Node`
```C
int findHeight(BstNode* root){
  if(root == NULL){
    return 0;
  }

  int leftHeight = findHeight(root->left);
  int rightHeight = findHeight(root->right);

  return (leftHeight > rightHeight ? leftHeight : rightHeight ) + 1;
}
```

