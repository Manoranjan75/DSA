# Maximum Sum of Non-Adjacent Elements (Dynamic Programming)

Given an array of integers, find the **maximum sum of elements such that no two chosen elements are adjacent**.

You may choose to **pick or skip** each element, but you cannot pick two neighboring elements.

---

## Example

- Input: [2, 1, 4, 9]
- Output: 11


Explanation:
- Pick `2` and `9` → sum = `11`
- Other options like `1 + 9 = 10` or `2 + 4 = 6` are smaller.

---

## Approach (DP – Space Optimized)

This problem is equivalent to the **linear House Robber** problem.

### DP Relation

Let:
- `dp[i]` = maximum sum considering elements up to index `i`

At index `i`, we have two choices:
1. **Include** current element  
   → `dp[i-2] + arr[i]`
2. **Exclude** current element  
   → `dp[i-1]`

So:
dp[i] = max(dp[i-1], dp[i-2] + arr[i])


### Space Optimization

Instead of using a DP array, we only need:
- `prev1` → `dp[i-1]`
- `prev2` → `dp[i-2]`

---

## Algorithm Steps

1. If the array has only one element, return it.
2. Initialize:
   - `prev2 = 0`
   - `prev1 = arr[0]`
3. Iterate from index `1` to `n-1`:
   - `include = prev2 + arr[i]`
   - `exclude = prev1`
   - `current = max(include, exclude)`
   - Update `prev2 = prev1`, `prev1 = current`
4. Return `prev1` as the answer.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)` (constant extra space)

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxNonAdjacentSum(vector<int>& arr) {
    int n = arr.size();

    if (n == 0)
        return 0;
    if (n == 1)
        return arr[0];

    int prev2 = 0;        // dp[i-2]
    int prev1 = arr[0];  // dp[i-1]

    for (int i = 1; i < n; i++) {
        int include = prev2 + arr[i];
        int exclude = prev1;
        int curr = max(include, exclude);

        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}

int main() {
    vector<int> arr = {2, 1, 4, 9};
    cout << "Maximum sum of non-adjacent elements: "
         << maxNonAdjacentSum(arr);
    return 0;
}
