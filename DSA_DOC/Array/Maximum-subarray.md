# Maximum Subarray (Kadane’s Algorithm) – C++

## Problem Statement

Given an integer array `nums`, find the **contiguous subarray** (containing at least one number) which has the **largest sum**, and return that sum.

This is also known as the **Maximum Subarray Problem** (LeetCode 53).

---

## Examples

### Example 1
```text
Input:  nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum = 6.

```
```cp
#include <bits/stdc++.h>
using namespace std;

int maxSubArray(vector<int>& nums) {
    int currentSum = nums[0];
    int maxSum = nums[0];

    for (int i = 1; i < nums.size(); i++) {
        // extend or restart
        currentSum = max(nums[i], currentSum + nums[i]);
        // update global maximum
        maxSum = max(maxSum, currentSum);
    }
    return maxSum;
}

int main() {
    vector<int> nums = {-2,1,-3,4,-1,2,1,-5,4};

    cout << "Maximum subarray sum: " << maxSubArray(nums) << endl;
    return 0;
}
