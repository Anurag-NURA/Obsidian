### Implementation using Array
```C
#include <stdio.h>
#include <stdbool.h>
#define MAX_SIZE 4

int arr[MAX_SIZE];
int top = -1;

void Push(int data){
  if(top == MAX_SIZE-1){
    printf("Error: Stack Overflow!!!\n");
    return;
  }
  arr[++top] = data;
  return;
}

void Pop(){
  if(top == -1){
    printf("Error: Stack Underflow!!!\n");
    return;
  }
  printf("\n%d popped", arr[top]);
  arr[--top];
}

void Peek(){
  printf("%d\n", arr[top]);
  return;
}

void main(){
  int response = true, choice, data;
  
  while (response) {
    printf("\n");
    printf("1. Push\n");
    printf("2. Pop\n");
    printf("3. Peek\n");
    printf("4. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
      case 1: printf("\nEnter a number: ");
              scanf("%d", &data);
              Push(data);
              printf("\n%d pushed in stack", data);
              break;
      
      case 2: Pop();
              printf("\nPop");
              break;

      case 3: Peek();
              break;
      
      case 4: printf("\nWARNING: Exiting the menu !!!");
              response = false;
              break;

      default:printf("Error Occured\n");
              break;
      }
  }

  printf("\n");
}
```

### Implementation using Linked List
```C
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

struct Stack{
  int data;
  struct Stack* next;
};

struct Stack* TOP;

void Push(int data){
  struct Stack* node = (struct Stack*)malloc(sizeof(struct Stack));
  node->data = data;
  node->next = NULL;

  if (TOP!=NULL) {
    struct Stack* temp = TOP;
    node->next = temp;
  } 
  TOP = node;
  return;
}

void Pop(){
  struct Stack* delete=TOP;

  if(TOP == NULL){
    printf("\nERROR: stack underflow!!!");
    return;
  }
  TOP = TOP->next;
  printf("\n%d removed from stack", delete->data);
  free(delete);
}

bool IsEmpty(){
  if (TOP == NULL) {
    return true;
  }else{
    return false;
  }
}

void Peek(){
  if(IsEmpty()){
    printf("\nStack is Empty");
    return;
  }else{
    printf("\nTOP----> %d", TOP->data);
    return;
  }
}

void main(){
  int response = true, choice, data;
  TOP = NULL;
  while (response) {
    printf("\n");
    printf("1. Push\n");
    printf("2. Pop\n");
    printf("3. Peek\n");
    printf("4. IsEmtpy?\n");
    printf("5. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
      case 1: printf("\nEnter a number: ");
              scanf("%d", &data);
              Push(data);
              printf("\n%d pushed in queue", data);
              break;
      
      case 2: Pop();
              printf("\nPop");
              break;

      case 3: Peek();
              break;
      
      case 4: if(IsEmpty()){
                printf("\nStack is Empty");
              }else{
                printf("\nStack is not Empty");
              }
              break;

      case 5: printf("\nWARNING: Exiting the menu !!!");
              response = false;
              break;

      default:printf("Error Occured\n");
              break;
      }
  }

  printf("\n");
}
```