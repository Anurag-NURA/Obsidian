As we know in a BST, all the values on the left sub-tree is _lesser_ then the __Root__ of the tree and values at the right sub-tree are greater. If this a Binary Tree does not follow this pattern then the BT is not a BST.

When a deleting a node we have to make sure that the pattern or this logic still maintains. 

1. **Have No Child:** Deleting a leaf node 
	![[Pasted image 20250521212114.png]]
Deleting a leaf node is easier as the leaf nodes are the last node of the tree, so delete the node from the end and remove the link, and also free up the memory, Simple!.

2. **Have One Child:** Delete a node in-between 
	![[Pasted image 20250522201957.png]]
	Now lets say, we want to delete **node 7** and we can see that it has only one child that is node with value 9. We will first link parent of node 7, i.e. node 5 with node 9 and then unlink node 7 and free the allocated memory.    
	
	When deleting a node whose child node have a subtree linked then also the scenario will be similar as then when we are setting (linking) node 5 with node 9 we basically are setting the marked subtree as right subtree of node 5 and that subtree is already in right of 5 so the system was already maintained.
	![[Pasted image 20250522203411.png]]
	
3. **Have Two Child:**  If we want to delete a node, let's say 15, then we cannot just remove the link and delete the node as other nodes linked through node 15 will also be unlinked and then they will consume space and we will have no way to access them again. 

	![[Pasted image 20250521214254.png]]

	Also we cannot just connect any one child with parent node as the other child node will be lost and the connected node with its subtree will become the new subtree for the parent node.
	![[Pasted image 20250522204749.png]]

So rather then removing the node from the tree we will clear or remove the value of the node we want to delete and add another value. 
![[Pasted image 20250522205145.png]]

That another value is *Minimum in right subtree*, i.e. **In-Order successor**. In our case 17 is that value. Then we will have two duplicate values. 

As we can observe now there are two nodes with same value of 17 but the node has only one child linked to it so deleting a node with one child is much easier compare to node with two child nodes. 
-  In a BST if a value is minimum then it won't have any node because if it will have any child node then that child's node value becomes the minimum value of the BST. 
- Similarly, in the right subtree the maximum value would be the last node of the BST and if it has any child node then the value of that child node is the maximum value of the BST.

So from two points mentioned above, selecting Minimum in right subtree is better as all the values are then maintained according to BST. But if we want we can select and replace the target node value with its *Maximum in left subtree* (**In-Order predecessor**). 
![[Pasted image 20250522213949.png]]

Then finally delete the Duplicate from left/right subtree accordingly.

### Implementation

```C
//delete a node from the tree
struct BstNode* deleteNode(struct BstNode* root, int data){
	if(root == NULL){
	    return root;
	}else if(data < root->data){
	    root->left = deleteNode(root->left, data);
	}else if(data > root->data){
	    root->right = deleteNode(root->right, data);
	}else{
		//Wohoo... I found you, Get ready to be deleted
		//case 1: No Child
	    if(root->left == NULL && root->right == NULL){
			free(root);
		    root = NULL;
	    }
	     
		//case 2: One Child
		if(root->left == NULL){
			//left subtree is empty
			struct BstNode* temp = root;
			root = root->right;//point to right child 
			free(temp);
		}else if(root->right == NULL){
			//right subtree is empty
			struct BstNode* temp = root;
			root = root->left;
			free(temp);
		}
		else{
			//case 3: Two Children
			struct BstNode* temp = findMinValueNode(root->right);
			root->data = temp->data;
			root->right = deleteNode(root->right, temp->data);
		}
	}
	return root;//return the updated root pointer
}
```

```C
//find the minimum value node in a BST
struct BstNode* findMinValueNode(struct BstNode* root){
	struct BstNode* current = root;
	while(current && current->left != NULL){
	    current = current->left;
	}
	return current;
}
```
