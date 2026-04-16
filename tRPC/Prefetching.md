In the MERN stack, your frontend usually feels like a "waiting game": the page loads, a loading spinner appears, and _then_ `useEffect` starts fetching data.

**Prefetching** is the act of fetching data **before** the user actually sees the component or needs the data. The goal is to eliminate loading spinners entirely.

### 1. How it works with tRPC

Because tRPC is powered by **TanStack Query**, it has a built-in memory. Prefetching simply means "pre-filling" that memory.

1. **The Server** fetches the data while the page is still being prepared.
2. **The Server** "dehydrates" that data (turns it into a JSON object).
3. **The Browser** "rehydrates" that data into its own cache.
4. When your component calls `useQuery()`, the data is **already there**. No loading state, no spinner.

### 2. Two Common Ways to Prefetch

#### A. The "Hover" Prefetch (Client-Side)
Imagine a list of jobs. When a user hovers their mouse over a "View Details" button, you can tell tRPC to start fetching the details for that job.
By the time the user actually clicks the button (usually 200–400ms later), the data is already in the cache. To them, the page load feels **instant**.

#### B. The "Server-Side" Prefetch (Next.js)
Since you are using Next.js, you can prefetch data on the server before the HTML is even sent to the browser.

```ts
// Inside a Server Component
const helpers = createServerSideHelpers({
  router: appRouter,
  ctx: await createTRPCContext(),
});

// "Prefetch" the data
await helpers.user.getProfile.prefetch();

// Now, when the Client Component renders:
// const { data } = trpc.user.getProfile.useQuery(); 
// 'data' will be available IMMEDIATELY. isLoading will be false.
```

### 3. MERN vs. tRPC Prefetching

| **Feature**         | **MERN (Typical)**                                 | **tRPC + Next.js**                                       |
| ------------------- | -------------------------------------------------- | -------------------------------------------------------- |
| **User Experience** | Spinner → Data                                     | Instant Data                                             |
| **Fetching**        | Starts after component mounts.                     | Starts before component mounts.                          |
| **Effort**          | You have to manually pass props down or use Redux. | Handled automatically by the shared `QueryClient` cache. |

## Example

```ts
import { Suspense } from "react";
import { getQueryClient, trpc } from "@/trpc/server";
import { HydrationBoundary, dehydrate } from "@tanstack/react-query";

import Client from "@/app/Client";

const page = () => {
	const queryClient = getQueryClient();
	void queryClient.prefetchQuery(trpc.hello.queryOptions({ text: "Anurag" }));
	
	return (
		<HydrationBoundary state={dehydrate(queryClient)}>
			<Suspense fallback={<div>Loading...</div>}>
				<Client />
			</Suspense>
		</HydrationBoundary>
	);
};

export default page;
```


This code is the perfect real-world example of **Server-Side Prefetching** that we just discussed. Since you are coming from MERN, this is where the "Next.js Magic" happens.

Here is the step-by-step breakdown of what this file is doing:

### 1. The "Preparation" (`prefetchQuery`)

```ts
const queryClient = getQueryClient();
void queryClient.prefetchQuery(trpc.hello.queryOptions({ text: "Anurag" }));
```

- **What's happening:** Before the server sends any HTML to the browser, it creates a `queryClient` (that "brain" we talked about).
- **The Action:** It says, "Go run the `hello` procedure with the input `Anurag` right now on the server."
- **Result:** The data is fetched and stored inside the `queryClient` memory while still on the server.
### 2. The "Packing" (`dehydrate`)

```ts
<HydrationBoundary state={dehydrate(queryClient)}>
```

- **The Concept:** You can't send a complex JavaScript object (the `queryClient`) directly from the server to the browser. You have to "shrink-wrap" it.
- **Dehydrate:** This function takes the data inside the `queryClient` and turns it into a plain JSON object that can be embedded in the HTML.

### 3. The "Unpacking" (`HydrationBoundary`)

- **The Concept:** When the HTML reaches the user's browser, the `HydrationBoundary` acts as the receiver.
- **Rehydrate:** It takes that "shrink-wrapped" JSON and injects it into the **browser's** version of the `queryClient`.

### 4. The Result inside `<Client />`

Inside your `Client.tsx` file, you probably have something like this:
```ts
const { data } = trpc.hello.useQuery({ text: "Anurag" });
```

Because of the code you shared, when the user opens the page:
1. `data` is **already populated** with the result.
2. `isLoading` is **false** immediately.
3. The user **never sees** the `<div>Loading...</div>` fallback.

### Why use `Suspense` then?
You might wonder: _"If the data is prefetched, why do we need the Suspense fallback?"_
- **For this specific call:** You don't really need it because the data is ready.
- **For the future:** If the `<Client />` component decides to fetch _additional_ data that wasn't prefetched, or if the user clicks a button to load more, `Suspense` will handle those future loading states.