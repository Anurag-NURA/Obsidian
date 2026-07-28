Infosys walk in interview question

![[Pasted image 20260728204049.png]]![[Pasted image 20260728204155.png]]
![[Pasted image 20260728204208.png]]

## Brute Force solution
```cpp
int countValidPairs(vector<int>& a, int D, int M) {
    int n = a.size();
    int count = 0;
    
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if ((a[i] + a[j]) % D == 0 &&
                abs(a[i] - a[j]) % M == 0) {
                count++;
            }
        }
    }
    return count;
}
```


## Optimized Solution

1.  ***First Condition***: $$(a[i]+a[j])modD=0$$
Instead of finding both pairs why don't we consider `a[j]` is fixed and find `a[i]`.

lets say `a[j] = 7` and `D = 5`

### Step 1: Start with the original equation
Now, we have to simplify this given formula.

$$(a[i]+a[j])modD==0$$
$$(a[i]+7)mod5==0$$
### Step 2: Replace the actual number with its remainder
By using a property of modulo arithmetic
**A fundamental property is:** 
$$(x+y)modm=((xmodm)+(ymodm))modm$$
This means you are **allowed** to reduce each operand individually before adding.

$$((a[i]mod5)+(7mod5))mod5==0$$
$$((a[i]mod5)+2)mod5==0$$

Notice `a[j]` hasn't disappeared.
It has simply become its remainder.

### Step 3: Find the required remainder

 Now the interview trick. When you're processing the array, suppose the current element is

```
a[j] = 7
```

You already know

```
7 % 5 = 2
```

So you ask:

> **What remainder must the other number have so that the remainders add to a multiple of 5?**

That means you're solving
$$(x+2)mod  5=0$$ 
```
where, a[i]%D = x
```

Let's test every possible remainder.

| x   | (x+2)%5 |
| --- | ------- |
| 0   | 2       |
| 1   | 3       |
| 2   | 4       |
| 3   | 0 ✅     |
| 4   | 1       |

Only

```
x = 3
```

works.

So any number whose remainder is 3 is a valid partner.

For example

```
3
8
13
18
23
```

All have remainder 3.

### Step 4: Generalize it

Suppose

```
current remainder = r = a[j]%D
```

We need some remainder

```
need = a[i]%D
```

such that
$$(need+r)  modD=0$$ 
Move `r` to the other side (modular arithmetic):
$$ need≡−r(modD)$$
But we don't like negative remainders.
Instead,
$$−r≡D−r(modD)-r$$

Therefore
$$ need = (D-r)modD $$

That's exactly the formula.
Here:
- `r` or `remD` is the remainder of the **current** element (`a[j]`).
- `need` is the remainder that the **other** element (`a[i]`) must have.

```cpp
class Solution {
	long long countValidPairs(vector<long long> &a, int D, int M) {
	    int n = a.size();
	    map<pair<int, int>, long long> mp;
		long long ans = 0;
		
		for (long long x : a) {
			//  for overflow  protection,
			//  we  use ((x % M) + M) % M instead of just (x % M)
			int remM = ((x % M) + M) % M;
			int remD = ((x % D) + D) % D;
			
			int need = (D - remD) % D;
			
			ans += mp[{need, remM}];
			mp[{remD, remM}]++;
		}
		return ans;
	}
};
```