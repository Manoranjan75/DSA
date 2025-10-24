#  Fibonacci using Top-Down Dynamic Programming (Memoization) — C++

---

##  Problem Statement

Compute the **nth Fibonacci number**, where:

- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2)


A **naïve recursive** approach leads to redundant calculations and exponential time complexity.  
To optimize it, we use **memoization**, storing previously computed results.

---

##  Approach — Top-Down + Memoization

We use **recursion + a DP array** to store computed Fibonacci values.

### Steps:
1. Use recursion to compute `fib(n)`.
2. Create a `dp` array initialized with `-1` to store already computed values.
3. Before each recursive call, check if the value is already computed.
4. If computed, reuse it; otherwise, calculate and store it in `dp[n]`.
5. Return the final result.

---

## Complexity Analysis
### Type	Complexity
- Time	O(n) — each subproblem solved once
- Space	O(n) — recursion stack + dp array

---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Recursive Fibonacci function with memoization
int fibn1(int n, vector<int> &dp) {
    if (n <= 1) {
        return n; // base case
    }

    if (dp[n] != -1) {
        return dp[n]; // already computed
    }
    
    dp[n] = fibn1(n - 1, dp) + fibn1(n - 2, dp);
    return dp[n];
}

int main() {
    int n;
    cout << "Enter the number: ";
    cin >> n;

    vector<int> dp(n + 1, -1); // initialize dp with -1 (uncomputed)

    int ans = fibn1(n, dp);
    cout << "Fibonacci sum: " << ans << endl;

    return 0;
}
