# What's new in React 18
 - Automatic batching
 - Suspense on the server
 - New APIs for app and library developers

## Automatic Batching

**Batching** in React is the process of **grouping multiple state updates into a single re-render**. Instead of re-rendering the component after every `setState` or `setCount`, React collects the updates and performs **one render** with the final state.

The goal is to improve performance by avoiding unnecessary renders.


![[Pasted image 20260720105650.png]]

![[Pasted image 20260720105722.png]]

![[Pasted image 20260720105740.png]]

### With React 18 updates are batched automatically
![[Pasted image 20260720105843.png]]
Instead of batching 3 renders react only batches state updates and render only once at the end.


## Suspense on the Server

![[Pasted image 20260720110033.png]]

So server rendering is a technique where we render the app's html output of your react component and send that HTML from the server so that user have some UI to observe while the JS bundles are loading and before the app becomes active.

Now consider an event where one component is taking unusually longer time than other components. That component might be doing some bundle heavy task or waiting for a response or anything
![[Pasted image 20260720110432.png]] 

Before React 18, this could have been a bottleneck of the app and increase the time its takes to render a component. 
![[Pasted image 20260720110754.png]]
One slow component can slow down the entire app because server side rendering is like `All or nothing` thing. With react 18 we have support for #react-suspense on the server. With the help of this suspense function we can wrap the slow component of the app telling react to delay the loading of this slow component. 

![[Pasted image 20260720111100.png]]

And show a loading spinner while slow component is delayed
![[Pasted image 20260720111142.png]]

### Suspense on the server
- One slow part doesn't slow down the whole page
- Show initial HTML early and stream the rest
- Code splitting fully integrated with server rendering


## New APIs for app and library developers

Concurrent features
- startTranstition()
- useTransition()
- useDeferredValue()

some other APIs (mostly for libraries)
- useId() -> generates unique ids for the components
- useSyncExternalStore() 

# How to upgrade to React 18

![[Pasted image 20260720111849.png]]


