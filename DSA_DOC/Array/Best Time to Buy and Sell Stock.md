# Best Time to Buy and Sell Stock

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the *i-th* day.

You want to maximize your profit by choosing **a single day to buy one stock** and choosing a **different day in the future to sell that stock**.

Return the maximum profit you can achieve from this transaction.
If you cannot achieve any profit, return `0`.

---

## Examples

**Example :**

```
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
```



## Solution (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minval = INT_MAX;  // track the minimum price so far
        int profit = 0;        // track the maximum profit
        for(int i = 0; i < prices.size(); i++) {
            minval = min(prices[i], minval);              // update minimum buying price
            profit = max(profit, prices[i] - minval);     // update maximum profit
        }
        return profit;
    }
};

// Driver code
int main() {
    Solution sol;

    vector<int> prices1 = {7, 1, 5, 3, 6, 4};
    cout << "Test Case 1 -> Max Profit: " << sol.maxProfit(prices1) << endl; // Expected: 5

    

    return 0;
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(n)` → Single pass through the array.
* **Space Complexity:** `O(1)` → Only uses two variables (`minval`, `profit`).

---
