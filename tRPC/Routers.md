In tRPC, **Routers** are the organizational units of your API. If a [[Procedures]] is a single function (an endpoint), a **Router** is the collection of those functions, similar to how a "controller" or "route file" works in REST.

## 1. What a Router Does

A router groups related procedures under a single namespace. For example, you might have a `userRouter` for profile logic and a `postRouter` for blog content. These are then merged into one single **AppRouter** that your frontend uses to talk to the backend.

### 1. The Conceptual Shift

In Express, you define a path string like `/api/users/login`. In tRPC, you define a **nested object structure**.

| **Feature**      | **Express (REST)**              | **tRPC**                         |
| ---------------- | ------------------------------- | -------------------------------- |
| **Organization** | `app.use('/users', userRouter)` | `t.router({ user: userRouter })` |
| **Access**       | `fetch('/api/users/getById')`   | `trpc.user.getById.useQuery()`   |
| **Structure**    | Flat strings (URLs)             | Hierarchical Objects             |

### 2. How it looks in Code

In a tRPC setup, you usually have one "Root Router" that combines smaller, domain-specific routers.

**The "Sub-Router" (e.g., `userRouter.ts`):**


```typescript
// This is like your express.Router()
export const userRouter = t.router({
  getUser: t.procedure.query(() => { 
    return { name: "Alex" }; 
  }),
});
```


## Gemini said

In the MERN stack, you’re used to using `express.Router()` to group your routes (e.g., `authRoutes.js`, `postRoutes.js`). In **tRPC**, a **Router** serves the exact same purpose, but with a major superpower: **Type Safety.**

Think of a Router as a folder or a container that organizes your API logic.

### 1. The Conceptual Shift

In Express, you define a path string like `/api/users/login`. In tRPC, you define a **nested object structure**.

| Feature          | Express (REST)                  | tRPC                             |
| ---------------- | ------------------------------- | -------------------------------- |
| **Organization** | `app.use('/users', userRouter)` | `t.router({ user: userRouter })` |
| **Access**       | `fetch('/api/users/getById')`   | `trpc.user.getById.useQuery()`   |
| **Structure**    | Flat strings (URLs)             | Hierarchical Objects             |

---

### 2. How it looks in Code

In a tRPC setup, you usually have one "Root Router" that combines smaller, domain-specific routers.

**The "Sub-Router" (e.g., `userRouter.ts`):**
``` typescript
// This is like your express.Router()
export const userRouter = t.router({
  getUser: t.procedure.query(() => { 
    return { name: "Alex" }; 
  }),
});
```

**The "App Router" (The Master List):** This is where you merge everything together.
``` typescript
export const appRouter = t.router({
  user: userRouter,    // Becomes trpc.user...
  post: postRouter,    // Becomes trpc.post...
});

// This line is the "magic" - it exports the backend's 
// shape as a Type for the frontend to see.
export type AppRouter = typeof appRouter;
```