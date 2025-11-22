# Find Minimum Element in a Sorted and Rotated Array (C++)

## Problem Statement

You are given a **sorted array** that has been **rotated** at some unknown pivot.

The array contains **distinct integers**.

Your task is to find the **minimum element** in the array in **O(log n)** time.

### Example 1

- Input:  nums = [3, 4, 5, 1, 2]
- Output: 1
- Explanation: The original sorted array [1, 2, 3, 4, 5] was rotated.

```cpp
#include <bits/stdc++.h>
using namespace std;

int findMin(const vector<int>& nums) {
    int start = 0;
    int end = nums.size() - 1;

    while (start < end) {
        int mid = start + (end - start) / 2;

        // If mid element is greater than the last element,
        // then the minimum lies in the right half.
        if (nums[mid] > nums[end]) {
            start = mid + 1;
        } 
        // Otherwise, the minimum lies in the left half (including mid).
        else {
            end = mid;
        }
    }

    // start == end -> index of the minimum element
    return nums[start];
}

int main() {
    vector<int> nums1 = {3, 4, 5, 1, 2};
    vector<int> nums2 = {4, 5, 6, 7, 0, 1, 2};
    vector<int> nums3 = {1, 2, 3, 4, 5};

    cout << "Minimum in nums1: " << findMin(nums1) << endl;  // 1
    cout << "Minimum in nums2: " << findMin(nums2) << endl;  // 0
    cout << "Minimum in nums3: " << findMin(nums3) << endl;  // 1

    return 0;
}

