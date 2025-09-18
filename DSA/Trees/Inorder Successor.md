The **in-order successor** of a node in a **Binary Search Tree (BST)** is the node with the **smallest value greater than the given node**. Essentially, it's the next node in an **in-order traversal** of the BST.

**Case 1:** *Node has a right subtree* 
Go deep to leftmost node in right subtree OR find minimum in right subtree
**Case 2:** *No right subtree*
Go to the nearest ancestor for which given node would be in left subtree

```
        20
       /  \
      8    22
     / \
    4   12
       /  \
      10   14
```

- The **inorder successor of 8** is **10**.
- The **inorder successor of 10** is **12**.
- The **inorder successor of 14** is **20**.

```C
//Function for finding mimimum node in left subtree
BstNode* findLeftMin(struct BstNode* root){
	if(root == NULL) return NULL;
	while(root->left != NULL){
		root = root->left;
	}
	return root;
}

//Finding the node with the provided value in BST and return its address
BstNode* findNode(struct BstNode* root, int data){
	if(root == NULL || root->data == data){
		return root;
	}else if(data < root->data){
		return findNode(root->left, data);
	}else if(data > root->data){
		return findNode(root->right, data);
	}
}

BstNode* getSuccessor(struct BstNode* root, int data){
	//Search the node: O(h) where h is the height of the tree
	struct BstNode* target = findNode(root, data);
	if(target == NULL){
		printf("Node with data %d not found in the tree.\n", data);
		return NULL;
	}
	
	//case 1: Node has right subtree
	if(target-> right != NULL){
		return findLeftMin(target->right);
	}
	//case 2: No right subtree
	else{
		struct BstNode* successor = NULL;
		struct BstNode* ancestor = root;
		while(ancestor != target){
			if(target->data < ancestor->data){
			//so far this is the deepest node for which target node is in left
			successor = ancestor; 
			ancestor = ancestor->left;
			}else{
				ancestor = ancestor->right;
			}
		}
		return successor;
	}
}
```