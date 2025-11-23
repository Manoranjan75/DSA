# Intersection of Two Arrays (C++)

## Problem Statement
Given two integer arrays `nums1` and `nums2`, return an array containing their **intersection**.

- Each element in the result must be **unique**.
- The order of the result does not matter.

## Example

### Input
nums1 = [1, 2, 2, 1]
nums2 = [2, 2]


### Output
[2]


---

## Approach

We want **unique common elements**.

### Steps:

1. Insert all elements of `nums1` into a **set** (to remove duplicates).
2. Traverse `nums2`, and if an element is present in the set:
   - Add it to the result.
   - Erase from set to maintain uniqueness.
3. Return the result.

This gives **O(n)** average time due to hash set operations.

---

## C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    unordered_set<int> s(nums1.begin(), nums1.end());
    vector<int> result;

    for (int x : nums2) {
        if (s.count(x)) {
            result.push_back(x);
            s.erase(x);  // ensure uniqueness
        }
    }
    return result;
}

int main() {
    vector<int> nums1 = {4, 9, 5};
    vector<int> nums2 = {9, 4, 9, 8, 4};

    vector<int> ans = intersection(nums1, nums2);

    cout << "Intersection: ";
    for (int x : ans) cout << x << " ";
    cout << endl;

    return 0;
}
