# Find First and Last Occurrence of an Element using Binary Search (C++)

This program finds the **first** and **last occurrence** of a given element `k` in a **sorted array** using **Binary Search**.  
It’s more efficient than a linear search, with a time complexity of **O(log n)**.

---

## Concept

When `vec[mid] == k`, we **don’t stop immediately**:

- For **first occurrence**, move **left** → `end = mid - 1`  
- For **last occurrence**, move **right** → `start = mid + 1`

This ensures we find the **leftmost** and **rightmost** indices respectively.

---

##  Dry Run Example

```cpp
vector<int> vec = {0, 1, 1, 1, 5};
int k = 1;
First Occurrence: index 1

Last Occurrence: index 3


#include <bits/stdc++.h>
using namespace std;

int firstOccurrence(vector<int> &vec, int k) {
    int start = 0, end = vec.size() - 1, ans = -1;
    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (vec[mid] == k) {
            ans = mid;
            end = mid - 1;  // search left
        } else if (vec[mid] < k)
            start = mid + 1;
        else
            end = mid - 1;
    }
    return ans;
}

int lastOccurrence(vector<int> &vec, int k) {
    int start = 0, end = vec.size() - 1, ans = -1;
    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (vec[mid] == k) {
            ans = mid;
            start = mid + 1;  // search right
        } else if (vec[mid] < k)
            start = mid + 1;
        else
            end = mid - 1;
    }
    return ans;
}

int main() {
    vector<int> vec = {0, 1, 1, 1, 5};
    int k = 1;

    cout << "First Occurrence: " << firstOccurrence(vec, k) << endl;
    cout << "Last Occurrence: " << lastOccurrence(vec, k) << endl;
    return 0;
}
