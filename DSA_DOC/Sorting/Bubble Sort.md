#  Bubble Sort (C++)

---

##  Concept

**Bubble Sort** is one of the simplest sorting algorithms.  
It repeatedly **swaps adjacent elements** if they are in the wrong order —  
just like “bubbling” the largest element to the top after each pass.

### Example
- Unsorted: [5, 3, 8, 4, 2]
- After sorting: [2, 3, 4, 5, 8]


---

##  How It Works

1. Compare adjacent elements (`arr[j]` and `arr[j+1]`).
2. If `arr[j] > arr[j+1]`, **swap** them.
3. Repeat this process for all elements.
4. After each pass, the largest element moves to the end.
5. If no swaps happen during a pass, the array is already sorted — stop early.

---
| Case        | Time Complexity | Explanation               |
| ----------- | --------------- | ------------------------- |
| **Best**    | O(n)            | Already sorted (no swaps) |
| **Average** | O(n²)           | Typical case              |
| **Worst**   | O(n²)           | Reverse order             |
| **Space**   | O(1)            | In-place sorting          |


---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    bool swapped;

    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        // last i elements are already sorted
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        // if no swaps occurred, the array is already sorted
        if (!swapped) break;
    }
}

int main() {
    vector<int> arr = {5, 3, 8, 4, 2};

    cout << "Before sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    bubbleSort(arr);

    cout << "After sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    return 0;
}
