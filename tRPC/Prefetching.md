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