# React Suspense

## Definition
Suspense is a rendering mechanism that allows React to pause rendering when a component is not ready.

## How it works
- A component throws a Promise during render
- React catches it
- Finds nearest Suspense boundary
- Shows fallback UI
- Retries render when Promise resolves

```ts
<Suspense fallback={<SidebarSkeleton />}>
  <Sidebar />
</Suspense>

<Suspense fallback={<ChatSkeleton />}>
  <Messages />
</Suspense>
```
## Key Point
Suspense does NOT fetch data. It only controls rendering.

## Mental Model
Component → throws Promise → Suspense catches → fallback → retry

## Common Use Cases

- Code splitting (React.lazy)
- Data fetching (via libraries like React Query)
- Streaming UI (Next.js)

## Important
Suspense blocks the entire subtree under it.