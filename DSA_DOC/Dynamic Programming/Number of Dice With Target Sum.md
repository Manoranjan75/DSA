# Number of Dice With Target Sum 

You are given:
- `dice` → number of dice  
- `faces` → number of faces on each die (values from `1` to `faces`)  
- `target` → required sum  

Find the **total number of ways** to roll the dice such that the **sum of face values equals `target`**.

Each die is independent, and **order matters** (since each roll sequence is different).

---

## Example
- Input:
dice = 3, faces = 6, target = 12

- Output:
Number of ways: 25


---

## Core Idea

This is a **classic DP counting problem**.

For every die:
- You can choose any face value from `1` to `faces`
- Reduce the target accordingly
- Move to the next die

The problem breaks into **overlapping subproblems**, making it ideal for **Dynamic Programming with Memoization**.

---


## Time & Space Complexity

- **Time Complexity:** `O(dice × target × faces)`
- **Space Complexity:** `O(dice × target)` (DP table + recursion stack)

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

// Memoization function
long long solveMem(int dice, int faces, int target, vector<vector<long long>>& dp) {

  // Base cases
  if (target < 0)
      return 0;

  if (dice == 0 && target == 0)
      return 1;

  if (dice == 0 && target != 0)
      return 0;

  if (dice != 0 && target == 0)
      return 0;

  // If already computed
  if (dp[dice][target] != -1)
      return dp[dice][target];

  long long ans = 0;

  // Try all face values
  for (int i = 1; i <= faces; i++) {
      ans += solveMem(dice - 1, faces, target - i, dp);
  }

  dp[dice][target] = ans;
  return ans;
}

// Wrapper function
long long diceThrow(int dice, int faces, int target) {
  vector<vector<long long>> dp(dice + 1, vector<long long>(target + 1, -1));
  return solveMem(dice, faces, target, dp);
}

// Driver code
int main() {
  int dice = 3;
  int faces = 6;
  int target = 12;

  cout << "Number of ways: "
       << diceThrow(dice, faces, target) << endl;

  return 0;
}



