### Understanding Generics and Inferences 
When using React Typescript for frontend and trying to make a request using 

```Typescript
getJobById: builder.query({
  query: (jobId) => ({
	url: `${JOBS_URL}/${jobId}`,
	method: "GET",
  }),
}),
```

this will show undefined and when trying to debug the problem in the backend by console logging the `id`  with `console.log(req.params)` receiving in the backend you will see this in console.
![[Pasted image 20250331190613.png]]
rather than the actual `id` of the Job.

The problem lies in __Understanding RTK Query and Generics__
In RTK Query, when you define a query using , you can use generic types to explicitly define:
- The type of data you expect the query to return (the first generic parameter).
- The type of argument the query function will accept (the second generic parameter).

For example:
![[Pasted image 20250331190818.png]]

In our case we have to modify our code 
```typescript
getJobById: builder.query<any, string>({
  query: (jobId) => ({
	url: `${JOBS_URL}/${jobId}`,
	method: "GET",
  }),
}),
```

We also need to understand __How Typescript Handles Inference:__

lets consider we want to make a request in the backend for searching database for a specific `keyword`

```Typescript
searchJobs: builder.query({
  query: (keyword) => ({
	url: `${JOBS_URL}/search?keyword=${keyword}`,
	method: "GET",
  }),
}),
```

Now you might be thinking this code will not work as this is not explicitly providing generics like `<ReturnedDataType, QueryArgumentType>`. But this will work as the argument `keyword` is clearly being passed directly to the `query` function as part of the URL. 

The URL is simple and doesn’t rely on nested objects or ambiguous parameters.

The response type wasn’t explicitly referenced in our component (i.e., you might not have used  `data` extensively with strict typing).

__Conclusion:__
The key difference lies in how TypeScript infers types based on the complexity of the query and response. In simpler cases (like the search query), TypeScript can infer everything correctly. However, for more complex cases (like `getJobById`), it often requires explicit generics to avoid ambiguity.

