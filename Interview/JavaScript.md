Next time you go for a JavaScript interview, don’t forget to brush up on these concepts:  
  
Closures: What they are, and how they preserve lexical scope.  
  
Hoisting: How `var`, `let`, `const`, and function declarations behave.  
  
Event Loop: Call stack, microtasks, macrotasks, and how async code is executed.  
  
Promises: How they work and common pitfalls with chaining.  
  
Async/Await: Syntax sugar over promises, error handling, and best practices.  
  
Scope: Difference between global, function, and block scope.  
  
This Keyword: Behavior in different contexts (regular function, arrow function, object methods).  
  
Prototypes & Inheritance: How prototype chaining works.  
  
Call, Apply, Bind: Function borrowing and controlling this.  
  
Currying: Converting a function with multiple arguments into nested unary functions.  
  
Debouncing & Throttling: Optimizing performance in scroll/input events.  
  
Type Coercion: Loose vs strict equality, falsy/truthy values.  
  
Null vs Undefined: Key differences and when each is used.  
  
Event Delegation: How to handle events efficiently.  
  
`setTimeout` vs `setInterval`: Execution behavior and clear mechanisms.  
  
IIFE (Immediately Invoked Function Expression): Why and when it’s used.  
  
Modules (ES6): Named vs default exports, import/export syntax.  
  
Object Destructuring & Spread/Rest: Clean syntax for copying and unpacking.  
  
Memory Management: Garbage collection basics and memory leaks.  
  
Optional Chaining & `Nullish Coalescing`: Clean handling of deeply nested objects.  
  
Temporal Dead Zone (TDZ): Why accessing `let` or `const` before declaration throws an error.  
  
Pure Functions & Side Effects: Core to functional programming and clean code.  
  
Array Methods — map, filter, reduce, find, some, every: Interviewers love them.  

Array reversal using javascript.
  
Deep vs Shallow Copy: Using `structuredClone`, `JSON.parse(JSON.stringify(...))`, `spread syntax`, etc.  
  
Generators & Iterators: Lazy evaluation, yield, and custom iterable protocols.


Q. What will be the output of the following
```javascript
var a = {};
var b = 4;

a.b = 4;
a[b] = 4;
```

Answer: 
firstly, `a.b` = 4 this uses **Dot Notation**
`a["b"]` = 4

so the object becomes:
```js
{
  b: 4
}
```

the key is the string `"b"`, not the variable

Secondly, `a[b] = 4`
here `b` is a variable, and its value is `4`.

so it becomes:

```js
a[4]=4
```

But object keys in JS are always strings, so:
```js
a["4"] = 4
```

Finally, object `a` is:
```js
{
  b: 4,
  "4": 4
}
```


Q: Remove duplicate in array:
Answer: 

By using a `Set`
```js
function uniqueArray(arr){
	return[...new Set(arr)];
}
```

Why this works:
- `Set` removes duplicates
- Spread (`...`) converts it back to an array
- Keeps the original order
⏱ Time: **O(n)**  
💾 Space: **O(n)**

Without using any library:
```js

```





