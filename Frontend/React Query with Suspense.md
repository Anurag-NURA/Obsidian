## useQuery vs useSuspenseQuery

### useQuery
- returns isLoading, error, data
- manual loading handling

### useSuspenseQuery
- throws Promise if data not available
- works with Suspense
- no loading flags

## Internal Behavior

if (!data) → throw Promise

## Benefits
- cleaner components
- centralized loading UI
- integrates with Suspense

## Downsides
- less granular control
- can create waterfalls if misused

## Waterfall Problem
Sequential queries:  
query1 → suspends → query2 waits

Solution:
- useSuspenseQueries
- split components