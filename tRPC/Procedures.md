In the world of **tRPC (TypeScript Remote Procedure Call)**, a **Procedure** is essentially a function that lives on your server but can be called by your client as if it were a local function.

Think of it as the "endpoint" in a traditional REST API, but with built-in type safety and zero manual fetching logic.

## The Three Types of Procedures

Every procedure in tRPC falls into one of three categories based on what it does with your data:

| **Procedure Type** | **Purpose**                           | **REST Equivalent**     |
| ------------------ | ------------------------------------- | ----------------------- |
| **Query**          | Fetching data (read-only).            | `GET`                   |
| **Mutation**       | Creating, updating, or deleting data. | `POST`, `PUT`, `DELETE` |
| **Subscription**   | Listening to real-time data streams.  | WebSockets              |

### Example Code

Here is what a basic "Query" procedure looks like on the server:

```TypeScript
const userRouter = router({
  // 'getUser' is the procedure name
  getUser: publicProcedure
    .input(z.string()) // Validates that the input is a string (ID)
    .query(async (opts) => {
      const { input } = opts;
      const user = await db.user.findById(input);
      return user; // Automatically typed for the client!
    }),
});
```

## Why "Procedures" over "Endpoints"?

The magic of a tRPC procedure is **End-to-End Type Safety**.

- **No JSON overhead:** You don't have to manually define `fetch('/api/user')` or handle the response type.
- **Auto-completion:** When you type `trpc.getUser.useQuery(` on your frontend, your IDE will tell you exactly what arguments it needs and exactly what the return object looks like.
- **Single Source of Truth:** If you change the return type in your server procedure, your frontend will immediately show a TypeScript error until you fix it.

**Note:** Procedures are always defined within a [[Routers]]. You can think of a Router as a folder and a Procedure as the file inside it.