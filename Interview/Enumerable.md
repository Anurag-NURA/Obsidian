## What is an enumerable property?
enumerable means "capable of being counted, listed, or enumerated one by one"

Every property in a JavaScript object has **attributes** (also called property descriptors). One of those attributes is `enumerable`.

The `enumerable` attribute can be either:

- `true` → the property shows up when JavaScript "enumerates" (loops through) the object's properties.
- `false` → the property is hidden from most enumeration methods.

For example:

```js
const person = {
  name: "Anurag",
  age: 23,
};

console.log(Object.keys(person));
```

Output: 
```js
["name", "age"]
```

## Creating a non-enumerable property

```js
const person = {  name: "Anurag",};

Object.defineProperty(person, "salary", {  
	value: 50000,  
	enumerable: false,
});

console.log(person.salary);
```

Output:

```js
50000
```

The property exists.

But:

```js
console.log(Object.keys(person));
```

Output:

```js
["name"]
```

Notice that `salary` is hidden.

Even:

```js
for (const key in person) {  
	console.log(key);
}
```

prints

```js
name
```