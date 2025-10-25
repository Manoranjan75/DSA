#  Min Cost Climbing Stairs (Space Optimized DP) — C++

---

##  Problem Statement

You are given an array `cost` where `cost[i]` represents the cost to step on the *i-th* stair.  
You can climb **either one or two steps at a time**.  
You start from step `0` or step `1`, and your goal is to reach the **top** (just beyond the last stair).

Find the **minimum total cost** to reach the top.

---

##  Approach — Dynamic Programming (Space Optimization)

From the standard DP approach, we know:
- dp[i] = cost[i] + min(dp[i-1], dp[i-2])


But since we only depend on the **last two computed values**,  
we can replace the entire DP array with **two variables**:

- `prev1` → stores `dp[i-1]`
- `prev2` → stores `dp[i-2]`

This optimization reduces **space complexity from O(n) → O(1)**.

---

| Type      | Complexity                          |
| --------- | ----------------------------------- |
| **Time**  | O(n) — single linear traversal      |
| **Space** | O(1) — only constant variables used |

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Space optimized version
    int solve(vector<int> &cost, int n) {
        int prev2 = cost[0];
        int prev1 = cost[1];

        for (int i = 2; i < n; i++) {
            int curr = cost[i] + min(prev1, prev2);
            prev2 = prev1;
            prev1 = curr;
        }

        return min(prev1, prev2);
    }

    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        return solve(cost, n);
    }
};

int main() {
    Solution sol;
    vector<int> cost = {10, 15, 20};
    cout << "Minimum Cost to Climb Stairs: " << sol.minCostClimbingStairs(cost) << endl;
    return 0;
}
