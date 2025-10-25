#  Min Cost Climbing Stairs (Top-Down Dynamic Programming)

---

##  Problem Statement

You are given an array `cost` where `cost[i]` is the cost of stepping on the *i-th* stair.  
You can climb **either one or two steps** at a time.

You start from step `0` or `1`, and your goal is to reach the **top** (just beyond the last stair).

Find the **minimum total cost** to reach the top.

---

##  Example

**Input:**
- cost = [10, 15, 20]


**Output:**
- 15


**Explanation:**
- Start from step 1 → pay 15 → reach top ✅ (minimum cost = 15)  
- Start from step 0 → 10 + 20 = 30 ❌ higher cost  

---

##  Approach — Top-Down + Memoization

We define a recursive function `solve(cost, n)` that returns the **minimum cost to reach step n**.

###  Recurrence Relation:
- solve(n) = cost[n] + min(solve(n-1), solve(n-2))

### 🔹 Final Answer:
- min(solve(n-1), solve(n-2))


→ because you can end on either of the last two stairs.

###  Optimization:
Use a **dp array** initialized with `-1` to store computed results and prevent recomputation.

---

| Type      | Complexity                      |
| --------- | ------------------------------- |
| **Time**  | O(n) — each state computed once |
| **Space** | O(n) — recursion + dp array     |


---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int solve(vector<int> &cost, int n, vector<int> &dp) {
        if (n == 0) return cost[0];
        if (n == 1) return cost[1];

        if (dp[n] != -1) return dp[n];

        dp[n] = cost[n] + min(solve(cost, n - 1, dp), solve(cost, n - 2, dp));
        return dp[n];
    }

    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        vector<int> dp(n + 1, -1);

        return min(solve(cost, n - 1, dp), solve(cost, n - 2, dp));
    }
};

int main() {
    Solution sol;
    vector<int> cost = {10, 15, 20};

    cout << "Minimum Cost to Climb Stairs: " << sol.minCostClimbingStairs(cost) << endl;
    return 0;
}
