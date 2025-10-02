# Problem: Majority Element  

Given an array `nums` of size `n`, return the **majority element**.  
The majority element is the element that appears **more than ⌊n / 2⌋ times**.  

### Example:  
- Input: `[2,2,1,1,1,2,2]`  
- Output: `2`  

---

## Time and Space Complexity

| Approach               | Time Complexity          | Space Complexity                        |
|------------------------|------------------------|----------------------------------------|
| Sorting                | O(n log n)             | O(1) or O(n) depending on sort implementation |
| Hashing                | O(n)                   | O(n)                                   |
| Boyer–Moore Voting     | O(n)                   | O(1)                                   |


---

## C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

class solution {

public:

    // Approach 1: Sorting
    int majorityElement_1(vector<int> &nums){
        int start = 0;
        int end = nums.size();
        sort(nums.begin(), nums.end());
        int ans = (start + end) / 2;
        return nums[ans];
    }

    // Approach 2: Hashing
    int majorityElement_2(vector<int> &nums){
        unordered_map<int, int> freq;
        int size = nums.size();
        int k = size / 2;

        for(int num : nums){
            freq[num]++;
            if(freq[num] > k){
                return num;
            }
        }
        return -1;
    }

    // Approach 3: Boyer–Moore Voting Algorithm
    int majorityElement_3(vector<int> &nums){
        int count = 0;
        int candidate = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;  // pick a new candidate
            }
            count += (num == candidate) ? 1 : -1;
        }
        return candidate;
    }

};

int main(){
    vector<int> nums = {2,2,1,1,1,2,2};
    solution sl;

    int ans1 = sl.majorityElement_1(nums);
    int ans2 = sl.majorityElement_2(nums);
    int ans3 = sl.majorityElement_3(nums);

    cout << ans1 << " " << ans2 << " " << ans3 << " ";

    return 0;
}
