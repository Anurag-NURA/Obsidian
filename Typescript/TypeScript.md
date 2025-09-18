### React.Ref vs React.RefObject

### Dynamic Object Access with Typescript

```typescript
const value = state[name as keyof typeof initialState]
```

This line is **accessing a property from the `state` object** dynamically using a string key (`name`), and it uses **TypeScript type assertion** to make sure the compiler doesn’t complain.

If we use,
`const value = state[name]` this will give us an error because in our mapping file of array we will be having name as a key to a string which will give the compiler error stating

![[Pasted image 20250405201408.png]]

Just focus on the first line of snippet which states that 
![[Pasted image 20250405201521.png]]

✅ The Fix: `as keyof typeof initialState`

This is a **type assertion** that says:

> “Hey TypeScript, don’t worry — `name` is definitely one of the keys of `initialState`.”

#### Here's the breakdown:

- `typeof initialState`: gets the type of the `initialState` object.
- `keyof typeof initialState`: gives you a **union type of all keys** in the `initialState` (e.g. `"title" | "description" | "salary" | ...`).
- `name as keyof typeof initialState`: tells TypeScript to **treat `name` as one of those keys**.
- `state[...]`: now works because `state` is the same shape as `initialState`.


### Defining a React Component Function

Some common ways of defining a react component function in typescript involves some certain steps:

1. If it is a `child` component and uses `props` make sure to define the types of props the component will be receiving. We can define the type with `interface`.

```typescript
interface CustomChildProps {
	children: React.ReactNode; //if it is a wrapper component
	customFn: (parameter: string) => void; //if props passed is a void function
	className: string; //if parent component is passing a style props
	placeholder?: string; //if prop passed is optional
	ref?: React.Ref<HTMLInputElement>; //if a ref hook prop is passed from parent
}
```

2. Use the interface while defining the function

```typescript
export const ChildComponent: React.FC<CustomChildProps> = ({children, customFn, className}) => ({
	function callFunction {
		customFn();
	}
	return(
		<div className={className}>
			{children}	
		</div>
	)
})
```

_or we can use much cleaner syntax_

```typescript
export const ChildComponent = ({children, customFn, className}: CustomChildProps) => ({
	function callFunction {
		customFn();
	}
	return(
		<div className={className}>
			{children}	
		</div>
	)
})
```


### Compare Two objects and return object with their difference
```Typescript
const handleSubmit = async (e: React.FormEvent) => {
  e.preventDefault();

  const original = { username, email, contact, address };
  const changed: Partial<Record<keyof typeof original, string | number>> = {};

  const isValid = UserInfoFormSchema.safeParse(state);
  if (!isValid.success) {
    console.error("Validation errors:", isValid.error.format());
    return;
  }

  for (const key in original) {
    const typedKey = key as keyof typeof original;
    if (original[typedKey] !== state[typedKey]) {
      changed[typedKey] = state[typedKey] as string | number;
    }
  }

  if (Object.keys(changed).length === 0) {
    console.log("No changes detected.");
    return;
  }

  try {
    setButtonStatus("Saving...");
    await updateUserInfo(changed).unwrap();
    setButtonStatus("Saved");

    setTimeout(() => {
      setButtonStatus("Save Changes");
    }, 2000);
  } catch (err) {
    console.error("Error updating user info:", err);
    setButtonStatus("Error");
  }
};

```