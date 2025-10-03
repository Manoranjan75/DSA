## Question
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` **in-place**. The relative order of the elements may be changed.  

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.  

Return `k` *after placing the final result in the first `k` slots of `nums`*.  

**Note:**  
- The elements beyond index `k-1` do not matter.  
- You do not need to allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.  

---

## Example

**Input:**  
nums = [3,2,2,3,4,3,5], val = 3


**Output:**  
- After removing 3, array length = 4
- Array elements: 2 2 4 5


---

## C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

int removeElement(vector<int>& nums, int val) {
    int k = 0;  // pointer for next position to place non-val elements
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != val) {
            nums[k] = nums[i]; // place non-val element
            k++;
        }
    }
    return k; // number of elements left
}

int main() {
    vector<int> nums = {3,2,2,3,4,3,5};
    int val = 3;

    int k = removeElement(nums, val);

    cout << "After removing " << val << ", array length = " << k << endl;
    cout << "Array elements: ";
    for (int i = 0; i < k; i++) {
        cout << nums[i] << " ";
    }
    return 0;
}
