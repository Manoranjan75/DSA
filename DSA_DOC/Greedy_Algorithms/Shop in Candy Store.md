# Shop in Candy Store 

You are given:
- An array `candies[]` of size `N`, where each element represents the **price of a candy**.
- An integer `K`, which denotes the offer:
  > For every **1 candy you buy**, you can get **up to `K` candies for free**.

Your task is to compute:
1. The **minimum cost** required to buy all candies.
2. The **maximum cost** required to buy all candies.

---

## Key Idea (Greedy Strategy)

To solve this problem optimally, we use **sorting + two pointers**.

### For Minimum Cost
- Buy the **cheapest candy first**.
- For every candy bought, take **K most expensive candies for free**.
- This minimizes the total cost.

### For Maximum Cost
- Buy the **most expensive candy first**.
- For every candy bought, take **K cheapest candies for free**.
- This maximizes the total cost.

---

## Algorithm Steps

### Step 1: Sort the candy prices
- sort(candies)

### Step 2: Minimum Cost Calculation
- `buy` pointer starts from the beginning.
- `free` pointer starts from the end.
- Each time you buy one candy:
  - Add its price to `mini`
  - Move `buy` forward by 1
  - Move `free` backward by `K`

### Step 3: Maximum Cost Calculation
- `buy` pointer starts from the end.
- `free` pointer starts from the beginning.
- Each time you buy one candy:
  - Add its price to `maxi`
  - Move `buy` backward by 1
  - Move `free` forward by `K`

---

## Time & Space Complexity

- **Time Complexity:** `O(N log N)` (due to sorting)
- **Space Complexity:** `O(1)` (excluding output vector)

---

## C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> candyStore(int candies[], int N, int K) {
        sort(candies, candies + N);

        int mini = 0;
        int buy = 0;
        int free = N - 1;

        // Minimum cost
        while (buy <= free) {
            mini += candies[buy];
            buy++;
            free -= K;
        }

        int maxi = 0;
        buy = N - 1;
        free = 0;

        // Maximum cost
        while (free <= buy) {
            maxi += candies[buy];
            buy--;
            free += K;
        }

        return {mini, maxi};
    }
};

int main() {
    Solution obj;

    int candies[] = {3, 2, 1, 4};
    int N = 4;
    int K = 2;

    vector<int> result = obj.candyStore(candies, N, K);

    cout << "Minimum cost: " << result[0] << endl;
    cout << "Maximum cost: " << result[1] << endl;

    return 0;
}
