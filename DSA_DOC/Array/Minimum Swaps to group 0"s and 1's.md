# Minimum Swaps to Group All 1’s Together  


We want to find the **minimum number of swaps** needed to bring all **1’s** together in an array consisting of **0’s and 1’s**.

Example:
- Input: 1 0 1 0 1
- Goal: 1 1 1 0 0
- Minimum swaps required = 1


---

##  Approach (Sliding Window on Count of 1’s)

Key idea:

1. Count total number of `1`s → this gives the **window size**.
2. We want the window of size `total_ones` that contains the **maximum 1s**.
3. Because:
   - If a window already contains many `1`s, fewer swaps are needed to fill the remaining with 1s.
4. Minimum swaps =  total_ones − max_ones_in_any_window_of_size_total_ones.


This works because:
- Swapping positions is equivalent to grouping.
- We only care about **how many 1s are already inside the window**.

---

## ⏳ Time & Space Complexity
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`  
(just counts and sliding window)

---

## Code

```cpp
#include<bits/stdc++.h>
using namespace std;

int minimum_swaps(vector<int> vec) {
 int n = vec.size();
 int total_ones = 0;

 // Count total number of 1's
 for (int i : vec) {
     if (i == 1) 
         total_ones++;
 }

 int max_ones = 0, curr_ones = 0;

 // Count 1's in first window
 for (int i = 0; i < total_ones; ++i) {
     if (vec[i] == 1) 
         curr_ones++;
 }

 max_ones = curr_ones;

 // Sliding window across rest of array
 for (int i = total_ones; i < n; ++i) {
     if (vec[i - total_ones] == 1) 
         curr_ones--;

     if (vec[i] == 1) 
         curr_ones++;

     max_ones = max(curr_ones, max_ones);
 }

 // Minimum swaps needed
 return total_ones - max_ones;
}

int main() {
 vector<int> vec = {1, 0, 1, 0, 1};
 cout << "Minimum swaps required: " << minimum_swaps(vec);
 return 0;
}

   
