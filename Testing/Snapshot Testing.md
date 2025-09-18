Snapshot testing captures the output (often rendered UI or JSON) of a component or function and compares it against a stored “snapshot file” that is human-readable and checked into version control. If the output changes unexpectedly, the test fails, prompting you to review whether these changes are intentional.

Eg. user.ts
```ts
export function fetchData(userId: string) {
	return {
		id: userId,
		name: "John Doe",
		roles: ["admin", "user"],
		lastLogin: new Date("2023-10-01T12:00:00Z").toISOString(),
		preferences: {
		  theme: "dark",
		  notifications: true,
		},
	};
}
```

user.test.ts
```ts
import { describe, test, mock } from "node:test";
import assert from "node:assert";
import { fetchData } from "../src/user.ts";

describe("User feature test 1", () => {
	test("fetches data from the server", () => {
		const data = fetchData("12345");
		assert.strictEqual(data.id, "12345");
		assert.strictEqual(data.name, "John Doe");
		assert.deepStrictEqual(data.roles, ["admin", "user"]);
		assert.strictEqual(data.lastLogin, "2023-10-01T12:00:00.000Z");
		assert.deepStrictEqual(data.preferences, {
			theme: "dark",
			notifications: true,
		});
	});
});

describe("User feature test 2", () => {
	test("fetches data with different userId", (t) => {
		const data: {
			id: string;
			name: string;
			roles: string[];
			lastLogin: string;
			preferences: {
				theme: string;
				notifications: boolean;
			};
		} = fetchData("12345");
		t.assert.snapshot(data);
	});
});

```

now when first time running this test on your system use command
```bash
node --test --test-update-snanpshots
```

![[Pasted image 20250725181256.png]]After that a snapshot of the fetched data will be saved and then will be used to test the other test cases. After this we can use normal command
```bash
node --test
```