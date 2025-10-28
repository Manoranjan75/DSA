#  Quick Sort (C++)

---

##  Concept

**Quick Sort** is a **Divide and Conquer** algorithm — similar to **Merge Sort**,  
but it works **in-place** (does not require extra arrays).

It selects a **pivot element** and partitions the array such that:

- Elements **less than** the pivot go to the **left**  
- Elements **greater than** the pivot go to the **right**

Then, it recursively sorts the left and right halves.

---

##  How It Works

1. Choose a **pivot** (commonly the last element).  
2. **Partition** the array:
   - Move all smaller elements before the pivot.  
   - Move all larger elements after it.  
3. Recursively apply the same steps to the left and right subarrays.  

---
| Case        | Time Complexity | Explanation                                       |
| ----------- | --------------- | ------------------------------------------------- |
| **Best**    | O(n log n)      | Balanced partitioning                             |
| **Average** | O(n log n)      | Typical case                                      |
| **Worst**   | O(n²)           | Unbalanced partition (e.g., already sorted array) |
| **Space**   | O(log n)        | Recursive call stack                              |
| **Stable**  | ❌ No            | Equal elements may change order                   |


---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Partition function: places pivot at correct position
int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[high];  // choose last element as pivot
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]); // place pivot correctly
    return i + 1;
}

// Quick Sort function
void quickSort(vector<int> &arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // partition index

        quickSort(arr, low, pi - 1);  // sort left subarray
        quickSort(arr, pi + 1, high); // sort right subarray
    }
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};

    cout << "Before sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    quickSort(arr, 0, arr.size() - 1);

    cout << "After sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    return 0;
}
