# 3Sum 

## Problem Statement

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that:

* `i != j`,
* `i != k`,
* `j != k`, and
* `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must **not contain duplicate triplets**.

---

## Examples

**Example :**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0
```



## Solution (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        int n = nums.size();
        sort(nums.begin(), nums.end());

        for(int i = 0; i < n - 2; i++) {
            if(i > 0 && nums[i] == nums[i-1]) continue; // skip duplicates

            int left = i + 1;
            int right = n - 1;

            while(left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if(sum == 0) {
                    ans.push_back({nums[i], nums[left], nums[right]});

                    // skip duplicates for left and right
                    while(left < right && nums[left] == nums[left+1]) left++;
                    while(left < right && nums[right] == nums[right-1]) right--;

                    left++;
                    right--;
                }
                else if(sum < 0) left++;
                else right--;
            }
        }

        return ans;
    }
};

// Driver code
int main() {
    Solution sol;

    // Test Case 1
    vector<int> nums1 = {-1,0,1,2,-1,-4};
    vector<vector<int>> res1 = sol.threeSum(nums1);
    cout << "Test Case 1 -> Triplets:" << endl;
    for(auto &triplet : res1) {
        cout << "[" << triplet[0] << ", " << triplet[1] << ", " << triplet[2] << "]" << endl;
    }
    // Expected: [-1,-1,2], [-1,0,1]

   
    return 0;
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(n^2)`

  * Sorting takes `O(n log n)`
  * Two-pointer approach for each element → `O(n^2)` overall.

* **Space Complexity:** `O(1)` (excluding output storage).

  * We only use a few pointers and variables, but output storage depends on the number of triplets.

---
