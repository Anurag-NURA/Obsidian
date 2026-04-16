# React Query Hydration

## Problem
Server fetch + Client fetch again = duplicate requests

## Solution Flow
1. Server: prefetchQuery()  [[Prefetching]]
2. Server: dehydrate()
3. Client: HydrationBoundary restores cache

## Result
- client already has data
- no refetch
- instant render

## Key Insight

Hydration = sharing server cache with client