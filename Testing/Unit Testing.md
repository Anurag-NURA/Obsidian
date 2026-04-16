### 🔍 **Key Points:**

- A **unit** is typically the smallest testable part of an application, such as a function, method, or class.
- **Unit tests** are small, fast, and focused.
- They are usually **automated** and written by developers during development.

### ✅ **Purpose of Unit Testing:**

1. **Verify correctness** of each unit.
2. Catch bugs early in development.
3. Make **refactoring safer**, as tests confirm that behavior hasn’t broken.
4. Improve **code quality** and reliability.

```ts
// function to test
export function add(a: number, b: number): number {
  return a + b;
}

// test case using Jest
test('adds two numbers', () => {
  expect(add(2, 3)).toBe(5);
});
```

Another example: 
greet.ts
```ts
export function greet(name: string): string {
  return `Hello, ${name}!`;
}
```

greet.test.ts
```ts
import { test } from "node:test";
import { strict as assert } from "node:assert";

import { greet } from "../greet.ts";

test("greet returns the correct greeting", () => {
  ///3A's
  /*
   * Arrange
   * Act
   * Assert
   */
  const expected = "Hello, Alice!";
  const actual = greet("Alice");
  assert.strictEqual(actual, expected, "The greeting should be correct");
});
```


### Isolation in Unit testing
**Isolation in unit testing** means testing a **single unit (e.g., function, method, or class)** **without involving its real dependencies** — so the test only verifies **that unit's behavior**, not the behavior of the system around it.
### ✅ In simple terms:
> Isolation = “Test one thing, and fake the rest.”


We will use **Dependency Injection (DI)** here. It is a software design pattern where **external dependencies** (like functions, classes, or services) are **passed into a component**, rather than being created or imported directly by it.

## 💡 Real-World Analogy:
Imagine you're a chef (`processOrder`) who needs a knife (`processPayment`).  
Instead of **buying your own knife**, someone **hands you a knife** when you're about to cook.

That way:
- You can **change the knife easily** (e.g. use a plastic one for training)
- You can **test the chef's skills independently** of which knife they use

order.ts
```ts
//this function will be tested in the testing file
export function processOrder(
	data: { amount: number },
	dependencies: {
		processPayment: (amount: number) => { id: string; amount: number };
	}
): { id: string; amount: number } {
	//some logic ...
	const paymentInfo = dependencies.processPayment(data.amount);
	return paymentInfo;
}

// this function will be mocked in the testing file
function processPayment(amount: number): {
	id: string;
	amount: number;
} {
	console.log("I am original....");
	return {
	id: "123",
	amount: amount,
	};
}
```

order.tests.ts
```ts
import { describe, mock, test } from "node:test";
import { strict as assert } from "node:assert";

import { processOrder } from "../order.ts";

describe("Order feature", () => {
	test("that it processes the order correctly", () => {
		const mockedProcessPayment = mock.fn((amount: number) => {
			//don't call any api or No side effects
			console.log("I am mocked....");
			return {
				id: "123",
				amount: amount,
			};
		});
		
		//Arrange
		const expected = { id: "123", amount: 3000 };
		
		//checking that the mock function has not been called yet
		//It is also known as SPY on a function
		assert.strictEqual(mockedProcessPayment.mock.callCount(), 0);
		
		//Act
		const result = processOrder(
			//passing the data
			{ amount: 3000 },
			//passing the dependencies
			{ processPayment: mockedProcessPayment }
		);
		
		//Assert
		assert.deepStrictEqual(result, expected);
		//checking that the mock function has been called once
		assert.strictEqual(mockedProcessPayment.mock.callCount(), 1);
		
		const call = mockedProcessPayment.mock.calls[0];
		assert.deepStrictEqual(call.arguments, [3000]);
	});
});
```