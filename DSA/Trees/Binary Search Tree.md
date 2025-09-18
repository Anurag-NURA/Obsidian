```C
bool Search(BstNode* root, int data){
  if(root == NULL) {
    return false;
  }
  else if(root->data == data) {
    return true;
  }
  else if(data<root->data) {
    return Search(root->left, data);
  }
  else {
    return Search(root->right, data);
  }
}
```

### Finding Minimum and Maximum value in a Binary Tree 
```C
int findMinValue(BstNode* root){
  if(root == NULL){
    printf("\nError: Tree is Empty!!!");
    return -1;
  }

  BstNode* current = root;
  while(current->left != NULL){
    current = current->left;
  }
  return current->data;
}

int findMaxValue(BstNode* root){
  if(root == NULL){
    printf("\nError: Tree is Empty!!!");
    return -1;
  }
  
  BstNode* current = root;
  while(current->right != NULL){
    current = current->right;
  }
  return current->data;
}
```

### Finding Minimum and Maximum value in a Binary Tree using Recursion:

```C
int findMinValueRecursion(BstNode* root){
  if(root == NULL) {  
    printf("\nError: Tree is Empty!!!");
    return -1;
  }

  if(root->left == NULL){
    return root->data;
  }

  return findMinValueRecursion(root->left);
}

int findMaxValueRecursion(BstNode* root){
  if(root == NULL) {  
    printf("\nError: Tree is Empty!!!");
    return -1;
  }

  if(root->right== NULL){
    return root->data;
  }

  return findMaxValueRecursion(root->right);
}

```