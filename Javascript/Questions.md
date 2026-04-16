### What are Promises?
### What are Callback functions?
_"I will call back later!"_
JavaScript functions are executed in the sequence they are called. Not in the sequence they are defined.

A **callback function** in JavaScript is a function that is **passed as an argument to another function** and is **executed after some operation has been completed**. It’s a way to ensure that a function runs **after another function finishes**, which is especially useful for asynchronous operations like fetching data, reading files, or handling user events.

#### Key Points:
1. **Functions are first-class citizens in JS**: This means you can pass functions around just like variables.
2. **Callbacks are used to handle asynchronous tasks**: For example, waiting for data from a server.
3. **They can be named or anonymous**.

Example 1: Synchronous Callback
```js
function greet(name) {
    console.log('Hello ' + name);
}

function processUserInput(callback) {
    const name = 'Alice';
    callback(name); // Call the callback function
}

processUserInput(greet); // Output: Hello Alice
```
Here, `greet` function is a callback function passed to `processUserInput`

Example 2: Asynchronous Callback
```js
console.log('Start');

setTimeout(function() {
    console.log('This is a callback after 2 seconds');
}, 2000);

console.log('End');
```

Output:
```bash
Start
End
This is a callback after 2 seconds
```
Here, the anonymous function inside `setTimeout` is a callback executed after 2 seconds.
### Explain the error in the code 
```javascript
class Person {
	constructor(name) {
		this.name = name;
	}
	
	fn() {
	    console.log(this.name);
	}
}

const person = new Person("Mr. X");
const copyFn = person.fn;
copyFn();
```

Error:
```js
TypeError: Cannot read properties of undefined (reading 'name')
```

Answer:
When you do:
```js
const copyfn = person.fn;
copyfn();
```

- The method `fn` is taken **out of its class context**.
- When you call `copyFn()`, `this` inside `fn` is **no longer bound** to the `person` instance.
- In strict mode (default for ES6 classes), `this` becomes `undefined`.
- So `this.name` throws the error.

**Fixes:**

✅1. Bind the method
```js
const copyFn = person.fn.bind(person);
copyFn(); // "Mr. X"
```

or 

```js
class Person{
	constructor(name){
		this.name = name;
		this.fn = this.fn.bind(this);
	}
	fn(){
		console.log(this.name);
	}
}
```

✅2. Use an arrow function inside the class

```js
class Person {
	constructor(name) {
		this.name = name;
	}
	
	fn = () => {
		console.log(this.name);
	}
}

const person = new Person("Mr. X");
const copyFn = person.fn;
copyFn(); // "Mr. X"
```

✅3. Call it on the instance
```js
person.fn();
```


### What are Pure Function ?

