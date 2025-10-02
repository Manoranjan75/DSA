# Problem: Check if Array is Rotated and Sorted  

We are given an array `nums`. We need to check whether the array is sorted in **non-decreasing order** and then **rotated** some number of times.  

### Example:  
- `[3,4,5,1,2]` → True (sorted array `[1,2,3,4,5]` rotated 3 times).  
- `[2,1,3,4]` → False.  
- `[1,2,3]` → True (already sorted and rotated 0 times).  

---
### Time and Space Complexity

#### Time Complexity: O(n)


#### Space Complexity: O(1)



---

## C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool check(vector<int>& nums) {
    int n = nums.size();
    int count = 0;

    for(int i = 0; i < n; i++) {
        if(nums[i] > nums[(i+1) % n]) {
            count++;
        }
        if(count > 1) return false;
    }
    return true;
}

int main() {
    vector<int> nums1 = {3,4,5,1,2};
    vector<int> nums2 = {2,1,3,4};
    vector<int> nums3 = {1,2,3};

    cout << check(nums1) << endl;  
    cout << check(nums2) << endl;  
    cout << check(nums3) << endl; 
}
