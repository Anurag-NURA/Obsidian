
# 1. The File Path

```ts
/api/trpc/[trpc]/route.ts
```

This is a **Next.js App Router API route**.

Equivalent Express idea:

```ts
/api/trpc/*
```

The `[trpc]` is a **dynamic route segment**.

Meaning this endpoint will handle requests like:

```ts
/api/trpc/post.getPosts  
/api/trpc/post.createPost  
/api/trpc/user.getUser
```

So **all tRPC calls go through this single endpoint**.

This replaces all of this:

```ts
/api/posts  
/api/users  
/api/comments
```

route.ts
```ts
import { fetchRequestHandler } from "@trpc/server/adapters/fetch";
import { createTRPCContext } from "@/trpc/init";
import { appRouter } from "@/trpc/routers/_app";

const handler = (req: Request) =>
  fetchRequestHandler({
    endpoint: "/api/trpc",
    req,
    router: appRouter,
    createContext: createTRPCContext,
  });

export { handler as GET, handler as POST };

/*
1. /api/trpc/[trpc]/route.ts is a Next.js App Router API route 
2. The [trpc] is a dynamic route segment.
3. 
*/
```

query-client.ts
```ts
import {
  defaultShouldDehydrateQuery,
  QueryClient,
} from "@tanstack/react-query";
import superjson from "superjson";

export function makeQueryClient() {
  //query client is like redux store for react-query, it holds the cache and configuration
  return new QueryClient({
    defaultOptions: {
      queries: {
        //hold the cached data for 30 seconds
        staleTime: 30 * 1000,
      },
      //this runs when server sends query data to browser(client)
      dehydrate: {
        //bacically normal json cannot serialize complex data types like dates, maps, sets, etc. superjson can handle these types and convert them to a format that can be safely transmitted over the network and then reconstructed on the client side.
        serializeData: superjson.serialize,

        /*Dehydration means next.js server will fetch data
        --> react query will cache it
        --> then sends the cached data to the browser(client)
        --> then react query on the client will use that cached data instead of making another request to the server.
        -->This improves performance and reduces unnecessary network requests.*/
        shouldDehydrateQuery: (query) => {
          //defaultShouldDehydreateQuery means only dehydrate successfull queries
          //"pending": This allows pending queries to be streamed to the client.
          return (
            defaultShouldDehydrateQuery(query) ||
            query.state.status === "pending"
          );
        },
      },
	hydrate: {
        deserializeData: superjson.deserialize,
      },
    },
  });
}

/* 
1. server components (runs api.post.getPosts()) 
2. React Query stores in cache (in server)
3. Dehyrdate the cache and send to client(browser): React query converts cache to JSON
4. Sent to browser: Embeded in HTML
5. Browser loads: React query runs superjson.deserialize
6. cache stored successfully in browser, no need to fetch data again from server, React query uses the cache to render the UI
*/
```


### 4. Create a tRPC client for Client Components

```ts
'use client';
 
import type { QueryClient } from '@tanstack/react-query';
import { QueryClientProvider } from '@tanstack/react-query';
import { createTRPCClient, httpBatchLink } from '@trpc/client';
import { createTRPCContext } from '@trpc/tanstack-react-query';
import { useState } from 'react';
import { makeQueryClient } from './query-client';
import type { AppRouter } from './routers/_app';
 
export const { TRPCProvider, useTRPC } = createTRPCContext<AppRouter>();
 
//this variable stores the cache outside React components.
let browserQueryClient: QueryClient;

//this function handles server vs browser behaviour
function getQueryClient() {
	//case 1: server (Next.js server components)
	//server renders run per request, so each request needs a fresh cache 
	//otherwise users could share data
	if (typeof window === 'undefined') {
		//if window does not exist -> we are on the server
		return makeQueryClient();
	}
	
	//case 2: Browser (Next.js client components)
	//browser should reuse the same cache
	if (!browserQueryClient) browserQueryClient = makeQueryClient();
	return browserQueryClient;
}
 
function getUrl() {
	const base = (() => {
	if (typeof window !== 'undefined') return '';
	if (process.env.VERCEL_URL) return `https://${process.env.VERCEL_URL}`;
		return 'http://localhost:3000';
	})();
	return `${base}/api/trpc`;
}
 
export function TRPCReactProvider(
	props: Readonly<{
	    children: React.ReactNode;
	}>,
) {
	//this creates or retrives the React Query cache
	const queryClient = getQueryClient();

	//creates the frontend API client (think of it like axios instance)	
	//httpBatchLink: this sends request to /api/trpc 
	//Request Batching: if multiple queries happen simultaneously
	const [trpcClient] = useState(() =>
	    createTRPCClient<AppRouter>({
			links: [
				httpBatchLink({
					// transformer: superjson, <-- if you use a data transformer
					url: getUrl(),
				}),
			],
		}),
	);
	return (
	<QueryClientProvider client={queryClient}>
		<TRPCProvider trpcClient={trpcClient} queryClient={queryClient}>
			{props.children}
		</TRPCProvider>
	</QueryClientProvider>
	);
}
```

This file is the **"Glue"** that connects your React frontend to your tRPC backend. It sets up two major systems at once: **TanStack Query** (handling caching/loading states) and **tRPC** (handling the typesafe communication).


A senior dev would mentally compress this entire file into **3 responsibilities**:

```
1️⃣ Create a React Query client (cache)
2️⃣ Create a tRPC client (API connection)
3️⃣ Provide both to the React app
```

### 1. `getQueryClient()`: The Brains of Caching

In MERN, if you fetch a user’s profile on two different pages, you might accidentally fetch it twice. `QueryClient` is a "brain" that remembers data so you don't have to refetch it constantly.
- **The logic inside:** Next.js runs code on both the **Server** (to pre-render) and the **Browser**.
- **The "Why":** On the server, we want a fresh "brain" for every request so users don't see each other's data. On the browser, we want to keep the **same** "brain" so that when you click "Back," the data is still there instantly.

### 2. `getUrl()`: Where is the Backend?

In Express, you might have `http://localhost:5000/api`. This function dynamically figures out where your API lives:
- If it's in the browser, it uses a relative path (`/api/trpc`).
- If it's on Vercel (production), it uses the production URL.
- If it's local development, it uses `localhost:3000`.

### 3. `httpBatchLink`: The Efficiency Expert

This is one of the coolest parts of tRPC.
- **In MERN:** If a page needs 5 different pieces of data, you make 5 different HTTP requests.
- **In tRPC:** `httpBatchLink` waits a few milliseconds, grabs all 5 requests, and sends them to the server in **one single flight**. It's like carpooling for your data.

### 4. `TRPCReactProvider`: The Wrapper

This is a **Context Provider**. You wrap your entire app (usually in `layout.tsx`) with this.
- It takes the "Brain" (`queryClient`) and the "Messenger" (`trpcClient`) and makes them available to every component in your app.
- Because of this, you can just call `const { data } = trpc.user.get.useQuery()` anywhere in your code without importing axios or setting up state.

### 5. Visual Architecture

```
App
 │
 ▼
TRPCReactProvider
 │
 ├─ QueryClientProvider
 │     │
 │     ▼
 │   React Query Cache
 │
 └─ TRPCProvider
       │
       ▼
   tRPC Client
       │
       ▼
   /api/trpc endpoint
```