Normally when we crate an object in JavaScript we are able to access it's field with data using dot operator. And cannot put any restriction on that plane JavaScript Object.

```javascript
const user = {
_id: 6214400424,
name: 'Anurag Rawat'
}

console.log(user.name)// 'Anurag Rawat'
```

**JavaScript Proxy** is an advanced feature that allows you to create custom behavior for fundamental operations on objects, such as property access, assignment, enumeration, and function invocation. 

The `Proxy` object wraps another object (the target) and intercepts operations performed on it.
`const proxy = new Proxy(target, handler)`
- `target`: The original object you want to wrap.
- `handler`: An object that defines custom behavior for various operations using __traps__.

```javascript
const target = {
  first_name: "Anurag",
  last_name: "Rawat"
}

const handler = {
	get: function(object, property){
		return property in object ? object[property]: `Property "${property}" does not exist`;
  }
};

const proxy = new Proxy(target, handler);
console.log(proxy.first_name); // console: Anurag
console.log(proxy.middle_name); // console: Property "middle_name" does not exist
```

Now in our example of a `user` we can hide some property using __Proxy__.

```javascript
const user = {
  _id: 6214400424,
  name: 'Anurag Rawat',
  age: 23,
}

const userProxy = new Proxy(user,{
	//the get intercepts property access
	get(target, property, receiver){
    const sensative = ['name', 'age'];
	    if(sensative.includes(property)){
	      console.log(`Accessing sensative property: ${property}`);
	    }
		return Reflect.get(...arguments);	
	},
})

console.log(userProxy.name); //console: Accessing sensative property: name
console.log(userProxy._id);//console: 621440024
```

Check out more !!!
![[Pasted image 20250402195116.png]]