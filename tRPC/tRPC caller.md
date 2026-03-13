In the MERN stack, you are used to the **Frontend** talking to the **Backend** over the network (HTTP). But what happens if your **Backend** needs to talk to **itself**?

A **tRPC Caller** is a way to execute your tRPC procedures (your API logic) directly, without making an actual HTTP request.

### 1. The "Why"

Imagine you have a tRPC procedure that fetches a user from MongoDB.

- **Normal way:** Your React component calls `trpc.user.get.useQuery()`. This sends an HTTP request from the browser to the server.
- **The Problem:** What if you are already _on the server_ (inside a Next.js Server Component or a Metadata function) and you want to use that same logic? Calling your own API over the internet is slow and redundant.

### 2. The Solution: The Caller

The **Caller** allows you to "call" your procedures as if they were just regular TypeScript functions.

- **No Network:** It doesn't use `fetch` or `axios`. It just runs the function code.
- **Type Safety:** It still checks your inputs and outputs.
- **Context:** It still uses the same `Context` (the JWT/User info) we talked about earlier.

### 3. How it looks in code

Remember the `createCallerFactory` line in the file you shared earlier? That’s what creates this.

**Inside a Next.js Server Component:**
```ts
// 1. Create the context (manually since there's no "request" yet)
const ctx = await createTRPCContext();

// 2. Create the "Caller" using your App Router
const createCaller = createCallerFactory(appRouter);
const caller = createCaller(ctx);

// 3. Call the procedure directly!
// This runs the code in your backend folder WITHOUT an HTTP request.
const user = await caller.user.getById({ id: '123' });
```

 
 In Server component the page will be first rendered and then it fill be fetching the data. But what if we can start fetching the data on the server and then continue using the data in the client component. That is [[Prefetching]].