![[Pasted image 20260729225502.png]]

From the question we understood that the min total cost for `ith` stairs will be the `difference between the height of the stair at current and the next stair to jump at`i.e., 

$$|height[i]-height[target]$$

We don't have to count the chair in between if the jump was for `(i+2)th` stairs.

lets solve this in a reverse fashion. Rather than thinking about minimum cost, we should focus on getting to the last stair. To get to the last `nth` stair we have two options. 
- Either take the last jump from `(n-1)th` stair to the `nth` stair.
![[Pasted image 20260729230154.png]]

- Or, take the last jump from `(n-2)th` stair for the `nth` stair.
![[Pasted image 20260729230302.png]]

Through this we can calculate the minimum cost. As if we already calculated the minimum cost to reach `(n-1)th` stair and same for `(n-1)th` stair. Now we have to only calculate the cost from `n-1` and `n-2` stairs to the `nth` stair.

Cost of jump from `(n-1)th` to `nth` stair is
$$|hight[n-1] - height[n]|$$
Similarly, Cost of jump from `(n-2)th` to `nth` stair is
$$|hight[n-2] - height[n]|$$

But we need to also consider the fact that their was minimum cost of climbing till `(n-1)th` stair and `(n-2)th` stair.

So equation becomes for `(n-1)th` stair
$$(n-1)^{min\_cost} + |height[n-1]-height[n]|$$

So equation becomes for `(n-2)th` stair
$$(n-2)^{min\_cost} + |height[n-2]-height[n]|$$
![[Pasted image 20260729232301.png]]

let's say we use a `dp` array as data structure to store the `min_cost` of each stair. Then,

$$dp[i] = min(dp[i-1] + (height[i]-height[i-1]), dp[i-2] + (height[i]-height[i-2]))$$

**Problem solved using Tabulation Dynamic Problem**
```cpp
#include <algorithm>
#include <cstdlib>
#include <iostream>
#include <vector>

using namespace std;

class Solution {
public:
  int minCostClimb(vector<int> &stairs) {
    int n = stairs.size();
    if (n == 1)
      return 0;

    vector<int> dp(n);

    dp[0] = 0;
    dp[1] = abs(stairs[0] - stairs[1]);

    for (int i = 2; i < n; ++i) {
      dp[i] = min(dp[i - 1] + abs(stairs[i] - stairs[i - 1]),
                  dp[i - 2] + abs(stairs[i] - stairs[i - 2]));
    }

    return dp[n - 1];
  }
};

int main() {
  Solution sol;
  vector<int> stairs = {30, 20, 50, 10, 40};

  cout << "\nMinimum cost for the frog to climb the stairs is "
       << sol.minCostClimb(stairs) << endl;

  return 0;
}

```