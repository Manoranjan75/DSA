# Aggressive Cows Problem

## Problem Statement
You are given an array `stalls[]` where each element represents the position of a stall on a straight line.  
You have `k` cows that need to be placed in these stalls such that **the minimum distance between any two cows is as large as possible**.

Your goal is to determine the **largest minimum distance** possible between the cows.

---

##  Example

### Input:
- stalls = [1, 2, 4, 8, 9]
- k = 3

### Output:
- 3


### Explanation:
- Place the 1st cow at stall position **1**  
- Place the 2nd cow at stall position **4**  
- Place the 3rd cow at stall position **8**  

The minimum distance between any two cows = **3**.  
No larger minimum distance is possible while placing all 3 cows.

---

##  Approach Explanation

### Intuition:
We want to maximize the **minimum distance** between any two cows.  
This type of problem can be solved efficiently using **Binary Search on the answer** — a technique often used when the answer lies in a monotonic search space.

---

### Algorithm Steps:

1. **Sort the stall positions.**
   - This ensures cows are placed in an ordered manner.

2. **Define the search space:**
   - `s = 0` → Minimum possible distance between cows.
   - `e = stalls[n-1] - stalls[0]` → Maximum possible distance.

3. **Apply Binary Search:**
   - Compute `mid = (s + e) / 2`.
   - Check if it is **possible** to place all cows such that the minimum distance between them is at least `mid`.

4. **Helper Function – `isPossible()`:**
   - Place the first cow at `stalls[0]`.
   - For each next stall, if the distance between the current stall and `lastPos` ≥ `mid`, place the next cow.
   - If all `k` cows are placed successfully, return `true`.

5. **Decision Making:**
   - If placing all cows is possible with `mid` distance, store it as a potential answer and try a larger distance (`s = mid + 1`).
   - Otherwise, try a smaller distance (`e = mid - 1`).

6. **Return the largest possible minimum distance.**

---

##  Time and Space Complexity

| Complexity | Explanation |
|-------------|--------------|
| **Time** | `O(n * log(max(stalls)))` — sorting + binary search with `O(n)` checking |
| **Space** | `O(1)` — only variables used |

---

##  Code (C++)

```cpp
#include <vector>
#include <algorithm>
using namespace std;

bool isPossible(vector<int> &stalls, int k, int mid, int n) {
    int cowCount = 1;
    int lastPos = stalls[0];
    
    for(int i = 0; i < n; i++) {
        if(stalls[i] - lastPos >= mid) {
            cowCount++;
            if(cowCount == k) {
                return true;
            }
            lastPos = stalls[i];
        }
    }
    return false;
}

int aggressiveCows(vector<int> &stalls, int k) {
    sort(stalls.begin(), stalls.end());
    int s = 0;
    int n = stalls.size();
    int e = stalls[n - 1];
    int ans = -1;
    int mid = s + (e - s) / 2;
    
    while(s <= e) {
        if(isPossible(stalls, k, mid, n)) {
            ans = mid;
            s = mid + 1;
        } else {
            e = mid - 1;
        }
        mid = s + (e - s) / 2;
    }
    return ans;
}
