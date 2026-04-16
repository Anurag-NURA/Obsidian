### Using Array
```C
#include <stdio.h>
#include <stdbool.h>
#define SIZE 5

int queue[SIZE];
int front = -1, rear = -1;

bool isFull(){
	return (front == (rear+1)%SIZE);
}

bool isEmpty(){
	return (front == -1);
}

void enqueue(int value){
	if(isFull()){
		printf("\nQueue is Full!!!");
	}else{
		if(isEmpty()){
		  front = 0;
		}
		rear = (rear+1)%SIZE;
		queue[rear] = value;
		printf("Inserted %d\n", value);
	}
}

int dequeue(){
	if(isEmpty()){
		printf("Queue is empty!!!");
		return -1;
	}else{
		int data = queue[front];
		if(front == rear){
			front = rear = -1;
		}else{
			front = (front + 1)%SIZE;
		}
		return data;
	}
}

void display(){
	if(isEmpty()){
		printf("\nQueue is empty!!!");
	}else{
		printf("\nQueue elements: ");
		int i = front;
		printf("\nFront-> ");
		while(true){
			printf("%d -> ", queue[i]);
			if(i==rear) break;
			i = (i+1)%SIZE; 
		}
		printf("Rear\n");
	}
}

void main(){
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);
    enqueue(50);  // Queue is full
    display();
    printf("Deleted %d\n", dequeue());
    enqueue(60);
    display();
	printf("\n");
}
```

### Using Linked List
```C
#include <stdio.h>
#include <stdlib.h>

struct LinkedList {
	int data;
	struct LinkedList* next;
};

struct LinkedList *front = NULL, *rear=NULL;

struct LinkedList* createNode (int data){
	struct LinkedList* newNode = (struct LinkedList*)malloc(sizeof(struct LinkedList));
	newNode->data = data;
	newNode->next = NULL;
	return newNode;
}

int isEmpty(){
	return front==NULL;
}

void enqueue(int value){
	struct LinkedList* newNode = createNode(value);
	
	//queue is emptu
	if(front==NULL){
		front = rear = newNode;
		rear->next = front; //cicular link    
	}else{
		rear->next = newNode;
		rear = newNode;
		rear->next = front;
	}
	
	printf("\nInserted value %d", value);
}


int dequeue(){
	if(isEmpty()){
		printf("\nQueue is Empty!!!");
		return -1;
	}
	
	int value;
		if(front==rear){
		value = front->data;
		free(front);
		front = rear = NULL;
	}else{
		struct LinkedList* temp = front;
		value = temp->data;
		front = temp->next; //assign next node in queue to the front
		rear->next = front; //maintain circular link
		free(temp);
	}
	return value;
}

void display(){
	if(isEmpty()){
		printf("\nQueue is Empty!!!");
		return;
	}
	
	struct LinkedList* temp = front;
	
	printf("\nQueue elements: \nFront -> ");
	do{
		printf("%d -> ", temp->data);
		temp = temp->next;
	} while(temp != front);
		printf("Rear\n");
}

int main() {
	enqueue(10);
	enqueue(20);
	enqueue(30);
	display();
	
	printf("Deleted %d\n", dequeue());
	display();
	
	enqueue(40);
	enqueue(50);
	display();
	
	return 0;
}
```