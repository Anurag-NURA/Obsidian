![[Pasted image 20260731200152.png]]
![[Pasted image 20260731200726.png]]
![[Pasted image 20260731200702.png]]


## Intuition

Similar question to LeetCode 1029 — Two City Scheduling

After calculating the cost of travel to City B, the question is asking pretty much the same thing. 
We will get two separate cost for each employee to travel either to city A or city B. 
![[Pasted image 20260801074646.png]]

In above example if we try to sort the value according to A values and assign index 1 and 2 to city A and index 3 and 4 to city B then we might get the min_cost like intended. But that isn't true for all the cases.

Another example
![[Pasted image 20260801075010.png]]

The min_cost value exceeded 530 which is not the right optimum answer. If we think lets sort it by B cost value we will get the right answer. But again it still won't be true for every cases. 

As this is not the actual parameter so what is the actual parameter then.
![[Pasted image 20260801075322.png]]

Lets look into another example 
![[Pasted image 20260801080357.png]]

what we need to calculate is the profit we would make more if we decide to send an employee to city A rather than to city B. So $CostA[i]-CostB[i]$ will help us calculate the difference between the two costs for an employee. More "positive" profit means we are maximizing the profit and minimizing the cost to spend. 

So when we sort the array by this profit in descending order we will array as we can see above in the example. Now we can choose employee with `[30, 300]` and `[40, 200]` for City A and employees with value `[20,60]` and `[10,50]` for city B. 

This entire process will take time (by using sorting) is `nlogn`. But this approach will be modifying the original cost array. If we are asked not to modify the cost array then in that case we will using a heap that also a max heap.

![[Pasted image 20260801114336.png]]

Each node will be having two values one will be `Profit` another one will be `Index`. The `top` of the max-heap will be the one with maximum profit. For the answer or `City A` we will pop first two nodes of the heap and add the values to the answer. And the remaining index (one which are not selected) will be Added to `City B` 


```cpp
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
  int minTravelCost(vector<int> &A, vector<int> &B, int N) {
    int total = 2 * N;
    vector<int> extraCost(total);
    long long answer = 0;

    // Initially send everyone to City A
    for (int i = 0; i < total; ++i) {
      answer += A[i];

      int cityBCost = min(A[i], B[i]) + B[i];
      extraCost[i] = cityBCost - A[i];
    }

    // Choose N employees with the smallest additional cost
    sort(extraCost.begin(), extraCost.end());

    for (int i = 0; i < N; i++) {
      answer += extraCost[i];
    }

    return answer;
  }
};

int main() {
  int N;
  cin >> N;

  int total = 2 * N;
  vector<int> A(total);
  vector<int> B(total);

  for (int i = 0; i < total; ++i) {
    cin >> A[i];
  }
  for (int i = 0; i < total; ++i) {
    cin >> B[i];
  }

  cout << "Minimum travel cost: " << Solution().minTravelCost(A, B, N) << endl;
  return 0;
}

```