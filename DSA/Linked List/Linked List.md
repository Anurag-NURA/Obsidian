```C
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

struct Node{
  int enroll;
  struct Node* next;
};

struct Node* HEAD;

void insertNodeAtBeginning(struct Node* data){
  if(HEAD!=NULL){
    (*data).next = HEAD;
  }else{
    (*data).next = NULL;
  }
  HEAD = data;
}

void insertNodeAtEnd(struct Node* data){
  if (HEAD==NULL) {
    HEAD = data;
    return;
  }

  struct Node* temp = HEAD;
  while ((*temp).next != NULL) {
    temp = (*temp).next;
  }
  (*temp).next = data;
  (*data).next = NULL;
}

void insertNodeAfterNth(struct Node* data, int target){
  if (HEAD==NULL) {
    HEAD = data;
    return;
  }

  struct Node* temp = HEAD;
  while((*temp).enroll != target){
    temp = (*temp).next;
  }
  (*data).next = (*temp).next;
  (*temp).next = data;
}

void insertNodeBeforeNth(struct Node* data, int target){
  if (HEAD==NULL) {
    HEAD = data;
    return;
  }
  
  if(HEAD->enroll == target){
    data->next = HEAD;
    HEAD = data;
    return;
  }

  struct Node* temp = HEAD;
  while(temp->next != NULL && temp->next->enroll != target){
    temp = temp->next;
  }
  data->next = temp->next;
  temp->next = data;
}

void deleteNodeFromBeginning(){
  struct Node* temp = HEAD;
  HEAD = HEAD->next;
  free(temp);
}

void deleteNodeFromEnd(){
  struct Node* temp = HEAD;
  while(temp->next->next != NULL){
    temp = temp->next;
  }
  struct Node* delete = temp->next;
  temp->next = NULL;
  free(delete);
}

void deleteSpecificNode(int target){
  if (HEAD->enroll == target) {
    deleteNodeFromBeginning();
    return;
  }

  struct Node* temp = HEAD, *delete;
  while (temp->next->enroll != target) {
    temp = temp->next;
  }
  delete = temp->next;
  temp->next = temp->next->next;
  free(delete);
}

void printLinkedList(){
  struct Node* temp = HEAD;
  printf("\nHEAD ---> ");
  if(HEAD!=NULL){
    while(temp != NULL){
      printf("| %d | ---> ", (*temp).enroll);
      temp = (*temp).next;
    }
  }else{
    printf("List is Empty!!!");
  }
  printf("NULL");
}

struct Node* setDetails(int enroll){
  struct Node* node = (struct Node*)malloc(sizeof(struct Node));
  (*node).enroll = enroll;
  (*node).next = NULL;
  return node;
}

void main(){
  int response = true, choice, enroll, target;
  HEAD = NULL;

  while (response) {
    printf("\n1. Insert at the Beginning");
    printf("\n2. Insert at the End");
    printf("\n3. Insert after a node");
    printf("\n4. Insert before a node");
    printf("\n5. Delete Node from Beginning");
    printf("\n6. Delete Node from the End");
    printf("\n7. Delete a specific Node");
    printf("\n8. Exit");
    printf("\nEnter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
      case 1: printf("\nEnter enroll number at the beginning: ");
              scanf("%d", &enroll);
              insertNodeAtBeginning(setDetails(enroll));
              printLinkedList();
              break;
      
      case 2: printf("\nEnter enroll number at the end: ");
              scanf("%d", &enroll);
              insertNodeAtEnd(setDetails(enroll));
              printLinkedList();
              break;

      case 3: printf("\nEnter enroll number: ");
              scanf("%d", &enroll);
              printf("\nEnter target to enter node after: ");
              scanf("%d", &target);
              insertNodeAfterNth(setDetails(enroll), target);
              printLinkedList();
              break;
      
      case 4: printf("\nEnter enroll number: ");
              scanf("%d", &enroll);
              printf("\nEnter target to enter node before: ");
              scanf("%d", &target);
              insertNodeBeforeNth(setDetails(enroll), target);
              printLinkedList();
              break;
      
      case 5: deleteNodeFromBeginning();
              printf("\nNode at the beginning deleted Successfully");
              printLinkedList();
              break;
      
      case 6: deleteNodeFromEnd();
              printf("\nNode at the end deleted Successfully");
              printLinkedList();
              break;

      case 7: printf("\nEnter Node to delete: ");
              scanf("%d", &target);
              deleteSpecificNode(target);
              printf("\nNode |%d| deleted Successfully", target);
              printLinkedList();
              break;

      case 8: printf("\nWARNING: Exiting the menu!!!");
              response = 0;
              break;

      default: printf("\nOhhhhh No, error occured!!!");
               break;
    }
  }

  printf("\n");
}
```