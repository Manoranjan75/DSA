# Fractional Knapsack Problem 

You are given:
- An array `wt[]` representing the **weights** of items
- An array `val[]` representing the **values** of items
- An integer `capacity` representing the **maximum weight** the knapsack can hold

Each item can be **broken into fractions**.  
Your task is to **maximize the total value** in the knapsack.

---

## Key Difference from 0/1 Knapsack

| 0/1 Knapsack | Fractional Knapsack |
|--------------|---------------------|
| Item is either taken fully or not taken | Item can be taken partially |
| Solved using DP | Solved using Greedy |
| NP-hard | Optimal greedy solution |

---

## Greedy Strategy (Core Idea)

To maximize value:
1. Compute **value-to-weight ratio** for each item: ratio = value / weight
2. **Sort items in descending order** of this ratio.
3. Start picking items:
- If the entire item fits → take it fully.
- Otherwise → take only the fraction that fits.

Why this works:
- Taking the item with the **highest value per unit weight first** always gives the optimal result.

---

## Algorithm Steps

1. For each item, compute: ratio = value / weight
2. Sort items by `ratio` in descending order.
3. Initialize `totalValue = 0`.
4. Traverse sorted items:
- If `weight <= capacity`:
  - Take full item
- Else:
  - Take fractional part:
    ```
    totalValue += ratio * capacity
    ```
  - Stop.

---

## Time & Space Complexity

- **Time Complexity:** `O(n log n)` (sorting)
- **Space Complexity:** `O(n)` (storing item ratios)

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
 static bool cmp(pair<double, pair<int,int>> a,
                 pair<double, pair<int,int>> b) {
     return a.first > b.first; // sort by ratio descending
 }

 double fractionalKnapsack(int capacity, vector<int>& wt, vector<int>& val) {
     int n = wt.size();
     vector<pair<double, pair<int,int>>> items;

     // Store {ratio, {value, weight}}
     for (int i = 0; i < n; i++) {
         double ratio = (double)val[i] / wt[i];
         items.push_back({ratio, {val[i], wt[i]}});
     }

     sort(items.begin(), items.end(), cmp);

     double totalValue = 0.0;

     for (int i = 0; i < n && capacity > 0; i++) {
         int weight = items[i].second.second;
         int value = items[i].second.first;

         if (weight <= capacity) {
             // Take full item
             totalValue += value;
             capacity -= weight;
         } else {
             // Take fractional item
             totalValue += items[i].first * capacity;
             capacity = 0;
         }
     }

     return totalValue;
 }
};

int main() {
 Solution obj;

 vector<int> val = {60, 100, 120};
 vector<int> wt  = {10, 20, 30};
 int capacity = 50;

 double ans = obj.fractionalKnapsack(capacity, wt, val);

 cout << fixed << setprecision(6) << ans << endl;

 return 0;
}


