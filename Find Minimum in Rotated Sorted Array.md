#  Find Minimum in Rotated Sorted Array (C++)

---

##  Problem Description

You are given a **sorted array of unique elements** that has been **rotated between 1 and n times**.  
Your task is to **find the minimum element** in this rotated array in **O(log n)** time.

A single rotation means moving the **last element to the front**.

**Example:**
- Original: [0, 1, 2, 4, 5, 6, 7]
- After 4 rotations → [4, 5, 6, 7, 0, 1, 2]


---

##  Key Idea

Since the array is rotated, it’s divided into two sorted parts:

- **Left part:** contains greater values  
- **Right part:** contains smaller values starting from the **minimum**

We use **Binary Search** to find the rotation point — which is the **smallest element**.

---

##  Binary Search Logic

1. Calculate  
- mid = start + (end - start) / 2


2. Compare `nums[mid]` with `nums[end]`:
- If `nums[mid] >= nums[end]` → the **minimum lies in the right half**, so `start = mid + 1`
- Else → the **minimum lies in the left half**, so `end = mid`

3. Continue until `start == end` → this index holds the **minimum element**.

---

##  Code

```cpp
class Solution {
public:
 int findMin(vector<int>& nums) {
     int start = 0;
     int end = nums.size() - 1;
     
     while (start < end) {
         int mid = start + (end - start) / 2;
         
         if (nums[mid] >= nums[end]) {
             start = mid + 1;    // search in right half
         } else {
             end = mid;          // search in left half (including mid)
         }
     }
     
     return nums[start];         // minimum element
 }
};

