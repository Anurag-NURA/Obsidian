### Important Terms
__Infix Expression__: Operators are placed __between__ operands. This is the standard notation we use in everyday math. 
Example: `A + (B * C)` 
A + BC *
ABC*+

__Prefix Expression (Polish notation)__:  Operators are placed before operands. No need for parentheses, as precedence is determined by order.
Example: `*+ABC`

__Postfix Expression (Reverse Polish notation)__: Operators come after operands. Like prefix, it removes the need for parentheses.
Example: `AB+C*`

### Order of Operation
- Parentheses: () {} [] (right to left)
- Exponents: (right to left)
- Multiplication and division (left to right)
- Addition and Subtraction (left to right)

![[Pasted image 20250317001640.png]]

### Infix to Postfix
__Rule 1:__ Check if the first character is an Operator or Operand. If it is an Operand append it to the Postfix string else if it is an Operator push it to the stack (let's say Operator Stack).
In our case first character was "A" so it was appended to the Postfix string

Now the second character is an Operator so it will be pushed to the stack. After that we again got an Operand 

![[Pasted image 20250317010454.png]]
![[Pasted image 20250317010509.png]]
![[Pasted image 20250317010530.png]]

### Implementation

Stack Implementation
```C
#include <stdio.h>
#include <stdbool.h>
#include <ctype.h>
#define MAX 10

char Infix[MAX], Postfix[MAX], Stack[MAX];
int top=-1;

void push(char x){
	Stack[++top] = x;
}

char pop(){
	if(top==-1){
		printf("Underflow!!!");
	}else{
		char item = Stack[top];
		Stack[--top];
		return item;
	}
}

char peek(){
	if(top == -1){
		printf("Stack is Empty");
	}else{
		return Stack[top];
	}
}

bool isEmpty(){
	if (top == -1){
		return true;
	}else{
		return false;
	}
}

```

Helper Functions
```C
bool isOperator(char c){
	return (c == '-' || c == '+' || c == '*' || c == '/');
}

bool isOperand(char c){
	return isalnum(c);
}

int precedence(char operator){
	int weight = -1;
	switch(operator){
		case '+': 
		case '-': weight = 1;
				  break;
					
		case '*':
		case '/': weight = 2;
				  break;
				
		default : break;
	}
	return weight;
}

bool hasHigherPrecedence(char op1, char op2){
	int w1 = precedence(op1);
	int w2 = precedence(op2);
	
	return w1 >= w2;
}
```

Infix to Postfix conversion function
```C
void InfixToPostfix(char exp[MAX]){
	int i, j=0;
	
	for (i=0; i<MAX;++i) {
		char c = exp[i];
		
		if(isOperand(c)){
			Postfix[j++] = c; 
		}else if(isOperator(c)){
			while(!isEmpty() && peek() != '(' && hasHigherPrecedence(peek(), c))
			{
				Postfix[j++] = pop();
			}
			push(c);
		}else if(c == '('){
			push(c);
		}else if(c == ')'){
			while(!isEmpty() && peek() != '('){
				Postfix[j++] = pop();
			}
			pop();
		}
	}
	while(!isEmpty()){
	    Postfix[j++] = pop();
	}  
}
```

Main Function
```C
void main(){
	printf("\nEnter Infix Expression: "); 
	scanf("%s", Infix);
	printf("\nInfix Expression: ");
	for(int i=0; i<10; ++i){
		printf("%c", Infix[i]);
	}
	
	InfixToPostfix(Infix);
	
	printf("\nPostfix Expression: ");
	for(int i=0; i<10; ++i){
		printf("%c", Postfix[i]);
	}
	
	printf("\n");
} 
```