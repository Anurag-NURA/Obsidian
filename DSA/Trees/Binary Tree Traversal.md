![[Pasted image 20250512092742.png]]

### Types of Traversal
1. Breadth-first
2. Depth-first

These are general techniques to traverse or search a _graph_. Tree is only a special type of graph.

![[Pasted image 20250512115632.png]]

### Level Order Traversal

![[Pasted image 20250512185516.png]]

Question is how can we visit the nodes in the above order in a program. There is no link from `D` node to `J` node and once we move from node `F` to `D` we cannot even come back to `F` node.

Solution can be that we can introduce a _Queue_. 
![[Pasted image 20250512185827.png]]

A node in the queue can be called __Discovered Node__. For example the very first discovered node will always be a `root` node, which is `F` node here. 
![[Pasted image 20250512190626.png]]

Then we will take out the node, which will be now `Visited` node, from the front and enqueue all the children of the root node. 
![[Pasted image 20250512190642.png]]

First we will enqueue the `left` child and then the `right` child. And before move from any node, we will first enqueue its children. 

![[Pasted image 20250512194715.png]]

Again we will first remove left node from the queue and then enqueue its children then remove the right node and enqueue its children. And so on till the last node in the tree. 

![[Pasted image 20250512195315.png]]


__Implementation:__
```C
//level order traversal
void levelOrder(struct BstNode *root){
	if(root ==  NULL){
	    return;
	}
	struct Queue q;
	initializeQueue(&q);
	enqueue(&q, root);
	  
	while(!isEmpty(&q)){
	    struct BstNode* current = dequeue(&q);
	    printf("%c", current->data);
	    
	    if(current->left != NULL){
	      enqueue(&q, current->left);
	    }
	    
	    if(current->right != NULL){
	      enqueue(&q, current->right);
	    }
	}
}
```

