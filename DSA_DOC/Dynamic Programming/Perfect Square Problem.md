# Perfect Square Problem — Minimum Number of Perfect Squares 

Given an integer `n`, determine the **minimum number of perfect square numbers**
(`1, 4, 9, 16, 25, ...`) whose **sum equals `n`**.

- You may use the same perfect square multiple times.
- Return the minimum count.

---

## Examples

- Input: n = 12
- Output: 3
- Explanation: 12 = 4 + 4 + 4


---

## Core Idea

This is a **Dynamic Programming** problem.

For a given number `n`, try subtracting **every perfect square ≤ n** and recursively solve the remaining value.  
Choose the option that gives the **minimum count**.

---

## DP Approach (Top-Down Memoization)

### Recursive Definition

Let `min_square(n)` be the minimum number of perfect squares required to form `n`.

- min_square(n) = 1 + min(
 min_square(n - 1²),
 min_square(n - 2²),
 min_square(n - 3²),
 ... )


### Base Case
- If `n == 0`, return `0` (no squares needed).

### Memoization
- Use a DP array `dp[]` where `dp[n]` stores the already computed answer for `n`.
- This avoids recomputation and drastically improves performance.

---

## Time & Space Complexity

- **Time Complexity:** `O(n * √n)`  
  (for each `n`, we try all squares up to `√n`)
- **Space Complexity:** `O(n)`  
  (DP array + recursion stack)

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

// Recursive function with memoization
int min_square(int n, vector<int> &dp){
    // Base case
    if(n == 0){
        return 0;
    }

    // If already computed
    if(dp[n] != -1){
        return dp[n];
    }

    int ans = n;  // Worst case: n times 1^2
    for(int i = 1; i * i <= n; i++){
        int square = i * i;
        ans = min(ans, 1 + min_square(n - square, dp));
    }

    dp[n] = ans;
    return dp[n];
}

// Wrapper function
int minSquares(int n) {
    vector<int> dp(n + 1, -1);
    return min_square(n, dp);
}

int main(){
    int num = 100;
    cout << minSquares(num);
    return 0;
}
