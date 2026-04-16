### Implementation using Arrays
```C
#include <stdio.h>
#include <stdbool.h>
#define MAX_SIZE 4

int arr[MAX_SIZE];
int front = -1, rear = -1;

bool IsEmpty(){
  if(front == -1 && rear == -1){
    return true; 
  }else{
    return false;
  }
}

void Enqueue(int data){
  if((rear+1)%MAX_SIZE == front){
    printf("Error: Queue Overflow!!!\n");
    printf("\nfront: %d", front);
    printf("\nrear: %d", rear);
    return;
  }else if(IsEmpty()){
    front = rear = 0;
    printf("\nfront: %d", front);
    printf("\nrear: %d", rear);
  }else{
    rear = (++rear)%MAX_SIZE;
    printf("\nfront: %d", front);
    printf("\nrear: %d", rear);
  }
  arr[rear] = data;
  return;
}

void Dequeue(){
  if(IsEmpty()){
    printf("Error: Queue Underflow!!!\n");
    return;
  }

  if(front == rear){
    printf("\n%d popped", arr[front]);
    front = rear = -1;
    return;
  }
  
  printf("\n%d popped", arr[front]);
  front = ++front%MAX_SIZE;
  return;
}

void Front(){
  if(front == -1){
    printf("\nQueue is Empty");
    return;
  }

  printf("%d\n", arr[front]);
  return;
}

void main(){
  int response = true, choice, data;
  
  while (response) {
    printf("\n");
    printf("1. Enqueue\n");
    printf("2. Dequeue\n");
    printf("3. Front\n");
    printf("4. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
      case 1: printf("\nEnter a number: ");
              scanf("%d", &data);
              Enqueue(data);
              printf("\n%d pushed in queue", data);
              break;
      
      case 2: Dequeue();
              break;

      case 3: Front();
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

struct Node{
  int data;
  struct Node* next;
};

struct Node* front = NULL;
struct Node* rear = NULL;

void Enqueue(int data){
  struct Node* temp = (struct Node*)malloc(sizeof(struct Node*));
  temp->data = data;
  temp->next = NULL;

  if(front == NULL && rear == NULL){
    front = rear = temp;
    return;
  }else{
    rear->next = temp;
    rear = temp;
  }
}

void Dequeue(){
  if(front == NULL && rear == NULL){
    printf("\nQueue is Empty");
    return;
  }
  struct Node* delete = front;
  front = front->next;
  free(delete);
}

void Front(){
  if (front == NULL) {
    printf("\nQueue is Empty");
    return;
  }

  printf("\n%d", front->data);
}

void printQueue(){
  struct Node* temp = front;

  printf("\n|Front|--->");
  while(temp != NULL) {
    printf("|%d|-->",temp->data);
    temp = temp->next;
  }

  if (front == NULL) {  
    printf("|NULL|-->");
  }

  printf("|Rear|");
}

void main(){
  int response = true, choice, data;
  
  while (response) {
    printf("\n");
    printf("1. Enqueue\n");
    printf("2. Dequeue\n");
    printf("3. Front\n");
    printf("4. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
      case 1: printf("\nEnter a number: ");
              scanf("%d", &data);
              Enqueue(data);
              printf("\n%d pushed in queue", data);
              printQueue();
              break;
      
      case 2: Dequeue();
              printQueue();
              break;

      case 3: Front();
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