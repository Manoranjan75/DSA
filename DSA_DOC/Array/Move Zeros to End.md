# Problem: Move Zeros to End  

Given an array `nums`, move all **zeros** to the **end** of the array while maintaining the relative order of the non-zero elements.  
You must do this **in-place** without making a copy of the array.  

### Example:  
- Input: `[1,2,0,0,3,0,0,0,4,0,5]`  
- Output: `[1,2,3,4,5,0,0,0,0,0]`  

---

### Time and Space Complexity
 #### Time Complexity: O(n)
 #### Space Complexity: O(1)

---

## C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

class solution{

public:

    void moveZeros(vector<int> &nums){
        int k = 0;  // Position to place the next non-zero element
        
        for(int i = 0; i < nums.size(); i++){
            if(nums[i] != 0){
                swap(nums[i], nums[k]);
                k++;
            }
        }
    }

    void print(vector<int> &nums){
        for(int num: nums){
            cout << num << " ";
        }
    }

};

int main(){
    vector<int> nums = {1,2,0,0,3,0,0,0,4,0,5};
    solution sl;
    sl.moveZeros(nums);
    sl.print(nums);

    return 0;
}
