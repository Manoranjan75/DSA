# Combination Sum (Counting All Ordered Combinations) 

You are given an array of **unique integers** `arr` and an integer `key` (target sum).  
Return the **total number of distinct combinations (sequences)** of elements from `arr` that sum up to `key`.

Important notes:
- Each element in `arr` can be used **multiple times**.
- **Order matters**: different sequences are counted as different combinations.

---

## Example
- Input:
- arr = [1, 2, 3]
- key = 4

- Output: 7

### Explanation  
All valid sequences that sum to `4` are:
(1, 1, 1, 1), (1, 1, 2), (1, 2, 1), (1, 3), (2, 1, 1), (2, 2), (3, 1)


Because order matters, `(1, 3)` and `(3, 1)` are counted separately.

---

## Core Idea (Dynamic Programming)

This is a **DP counting problem** similar to **Combination Sum IV**.

At any target value `key`, we try:
- Subtracting each element of `arr`
- Recursively counting the number of ways to form the remaining sum

---

## Recursive Relation (Top-Down DP)

Let `f(key)` be the number of combinations to form sum `key`.

f(key) = f(key - arr[0]) + f(key - arr[1]) + ... f(key - arr[n-1]).


### Base Cases
- `key == 0` → return `1` (one valid way: choose nothing)
- `key < 0` → return `0` (invalid combination)

### Memoization
- Use a DP array `dp[key]` to store results and avoid recomputation.

---

## Time & Space Complexity

- **Time Complexity:** `O(key × n)`  
  (`n` = size of array, each state computed once)
- **Space Complexity:** `O(key)`  
  (DP array + recursion stack)

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

int combination_sum(vector<int>& arr, int key, vector<int> dp){
    // Base cases
    if(key < 0){
        return 0;
    }
    if(key == 0){
        return 1;
    }

    if(dp[key] != -1){
        return dp[key];
    }

    int ans = 0;
    for(int i = 0; i < arr.size(); i++){
        ans += combination_sum(arr, key - arr[i], dp);
    }

    dp[key] = ans;
    return dp[key];
}

int combinationSum4(vector<int>& arr, int key) {
    vector<int> dp(key + 1, -1);
    int ans = combination_sum(arr, key, dp);
    return ans;
}

int main(){
    vector<int> vec = {9};
    int key = 3;

    cout << "Combination sum: " << combinationSum4(vec, key);
    return 0;
}

