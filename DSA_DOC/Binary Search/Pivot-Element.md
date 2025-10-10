#  Find the Pivot Element in a Rotated Sorted Array (C++)

This program finds the **pivot element** in a **rotated sorted array** using **Binary Search**.  
A pivot element is the **smallest element** in the array — the point where the rotation occurs.

---

##  Example
- [3, 4, 5, 1, 2] → Pivot = 1


Here, the sorted array `[1, 2, 3, 4, 5]` was rotated, and `1` marks the **rotation point**.

---

##  Concept

In a rotated sorted array:

- The **left half** (before pivot) is always **greater than or equal** to the first element.
- The **right half** (after pivot) contains **smaller elements**.

We use **binary search logic** to find where this change happens.

### Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int pivotElement(vector<int> &vec) {
    int start = 0, end = vec.size() - 1;

    while (start < end) {
        int mid = start + (end - start) / 2;

        if (vec[mid] >= vec[0]) {
            start = mid + 1;  // pivot lies in right half
        } else {
            end = mid;        // pivot lies in left half
        }
    }
    return start;  // index of pivot
}

int main() {
    vector<int> vec = {3, 4, 5, 1, 2};
    cout << "Pivot of an array: " << pivotElement(vec);
    return 0;
}





