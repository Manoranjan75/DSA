# Cut Rod into Segments of X, Y, Z (Dynamic Programming – Memoization)

You are given a rod of length `n` and three integers `x`, `y`, and `z` representing allowed segment lengths.  
Your task is to determine the **maximum number of segments** the rod can be cut into such that **each segment has length exactly `x`, `y`, or `z`**.  
If it is not possible to cut the rod exactly using these lengths, return `0`.

---

## Approach (DP with Memoization)

This is a classic **dynamic programming** problem similar to the **unbounded knapsack**.

At every rod length `n`, you have **three choices**:
- Cut a segment of length `x`
- Cut a segment of length `y`
- Cut a segment of length `z`

### Recursive Definition
Let `solve(n)` be the maximum number of segments for rod length `n`.
solve(n) = max(
solve(n - x),
solve(n - y),
solve(n - z)
) + 1


### Base Cases
- `n == 0` → return `0` (exact cut achieved)
- `n < 0` → return `INT_MIN` (invalid cut)

### Memoization
- Use a DP array `dp[]` where `dp[i]` stores the maximum number of segments for rod length `i`.
- If `dp[n]` is already computed, return it directly to avoid recomputation.

If the final result is negative, it means no valid segmentation exists → return `0`.

---

## Time & Space Complexity
- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(n)` (DP array + recursion stack)

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int solve(int n, int x, int y, int z, vector<int> &dp) {
    if (n == 0)
        return 0;
    if (n < 0)
        return INT_MIN;

    if (dp[n] != -1)
        return dp[n];

    int cutX = solve(n - x, x, y, z, dp);
    int cutY = solve(n - y, x, y, z, dp);
    int cutZ = solve(n - z, x, y, z, dp);

    dp[n] = max({cutX, cutY, cutZ}) + 1;
    return dp[n];
}

int cutSegments(int n, int x, int y, int z) {
    vector<int> dp(n + 1, -1);
    int ans = solve(n, x, y, z, dp);

    if (ans < 0)
        return 0;
    return ans;
}

int main() {
    int n = 7, x = 5, y = 2, z = 2;
    cout << "Maximum number of segments: "
         << cutSegments(n, x, y, z);
    return 0;
}
