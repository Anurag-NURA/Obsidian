#Dynamic-Programming, #DP is an optimization technique that solves problem with:
- **overlapping subproblems** - The solution to a problem can be constructed from solutions to its smaller subproblems.
- **optimal substructure** - The same subproblems are solved multiple times.

by storing intermediate results to avoid redundant computations

# Types:
## 1. Memoization

Applying dynamic programming through <u>recursion</u> is known as #memoization. It is also known as Top-down approach.

### Intuition

Suppose you compute `fib(5)` recursively.

```
fib(5)
├── fib(4)
│   ├── fib(3)
│   │   ├── fib(2)
│   │   └── fib(1)
│   └── fib(2)
└── fib(3)
```

Notice that

- `fib(3)` is computed twice.
- `fib(2)` is computed three times.

This repeated work makes the recursive solution inefficient.

Memoization stores the answer the **first time** a subproblem is solved. Whenever the same subproblem appears again, the stored value is returned instead of recomputing it.

*Fibonacci Series solved through Memoization*
```cpp
int fibDP(int n, vector<int> &f){
	if(n<=1) return n;
	
	if(f[n] != 1){
		return f[n];
	}
	
	return f[n] = fibDP(n-1,f) + fibDP(n-2,f);
}
```
## 2. Tabulation

Applying dynamic programming through <u>iteration</u> is known as #tabulation. It is also known as Bottom-up approach.

### Intuition

Instead of starting from `fib(n)` and recursively moving downward, we start from the smallest known answers.

We already know

```
fib(0)=0
fib(1)=1
```

Using these values, we compute

```
fib(2)
fib(3)
fib(4)
...
fib(n)
```

This is exactly how humans usually solve the problem.

*Fibonacci Series solved through Tabulation* 
```cpp
int fibTabDP(int n){
	vector<int> dp(n+1);
	dp[0] = 0;
	dp[1] = 1;
	
	for(int i=2; i<=n; ++i){
		dp[i] = dp[i-1] + dp[i-2];
	}
	return dp[n];
}
```

## Comparison

|Feature|Memoization|Tabulation|
|---|---|---|
|Approach|Top-Down|Bottom-Up|
|Uses recursion|Yes|No|
|Uses iteration|No|Yes|
|Computes only required states|Yes|No (usually computes all states up to the target)|
|Recursion stack|Yes|No|
|Easier to write|Usually|Sometimes more involved|
|Risk of stack overflow|Yes|No|

### Which One Should You Prefer?

- Use **memoization** when the recursive relation is natural and only a subset of states may be needed.
- Use **tabulation** when all states are required, when recursion depth could become large, or when you want to optimize space more easily.

For problems like Fibonacci, tabulation is generally preferred because it avoids recursion overhead.

## Some other Patterns are:

![[Pasted image 20260729112055.png]]

![[Pasted image 20260729112104.png]]