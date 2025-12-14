# House Robber (DP)

You are given an array `nums` where each element represents the amount of money in a house.  
You are a robber and **cannot rob two adjacent houses**.

In this version, **houses are arranged in a circle**, meaning:
- The **first and last houses are adjacent**.

Your task is to return the **maximum amount of money** you can rob without alerting the police.

---

## Key Observation (Circular Constraint)

Because the houses are circular:
- You **cannot rob both** the first and the last house.

So the problem is broken into **two linear subproblems**:
1. Rob houses from index `0` to `n-2` (exclude last house)
2. Rob houses from index `1` to `n-1` (exclude first house)

The final answer is the **maximum** of these two cases.

---

## DP Approach (Space Optimized)

For a **linear house robber problem**, the recurrence is:

- dp[i] = max(dp[i-1], dp[i-2] + nums[i])


Instead of using a DP array, we optimize space using two variables:
- `prev1` → dp[i-1]
- `prev2` → dp[i-2]

---

## Helper Function Explanation: `sumElement`

This function solves the **linear house robber problem** using space-optimized DP.

### Variables
- `prev1` → maximum sum till previous house
- `prev2` → maximum sum till house before previous

### At each step
- `inc = prev2 + nums[i]` (rob current house)
- `exc = prev1` (skip current house)
- Take the maximum

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)` (constant extra space)

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Helper function to solve linear house robber using space-optimized DP
int sumElement(const vector<int> &nums) {
    int n = nums.size();
    int prev2 = 0;        // dp[i-2]
    int prev1 = nums[0]; // dp[i-1]

    for (int i = 1; i < n; i++) {
        int inc = prev2 + nums[i]; // rob current house
        int exc = prev1;           // skip current house
        int ans = max(inc, exc);

        prev2 = prev1;
        prev1 = ans;
    }
    return prev1;
}

int rob(vector<int>& nums) {
    int n = nums.size();

    // Edge case: only one house
    if (n == 1) {
        return nums[0];
    }

    vector<int> first, second;

    // Case 1: exclude last house
    // Case 2: exclude first house
    for (int i = 0; i < n; i++) {
        if (i != n - 1) {
            first.push_back(nums[i]);
        }
        if (i != 0) {
            second.push_back(nums[i]);
        }
    }

    int ans = max(sumElement(first), sumElement(second));
    return ans;
}

int main() {
    vector<int> nums = {2, 3, 2};
    cout << "Maximum money robbed: " << rob(nums);
    return 0;
}


