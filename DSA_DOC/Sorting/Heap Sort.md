#  Heap Sort (C++)



##  Concept

**Heap Sort** is based on the **Binary Heap** data structure.  
It works by first building a **Max Heap**, where the largest element is at the root, and then repeatedly:

1. Swapping the root (maximum element) with the last node.  
2. Reducing the heap size.  
3. Re-heapifying to restore the **max-heap property**.

This process sorts the array in **ascending order**.

---

##  How It Works

1. **Build** a Max Heap from the input array.  
2. For each element from end to start:
   - Swap the root (largest) with the last element.
   - Reduce the heap size by 1.
   - Call `heapify()` to restore heap order.  
3. Repeat until the array is fully sorted.

---
| Case        | Time Complexity | Explanation                      |
| ----------- | --------------- | -------------------------------- |
| **Best**    | O(n log n)      | Heapify operations               |
| **Average** | O(n log n)      | Same for all inputs              |
| **Worst**   | O(n log n)      | Consistent performance           |
| **Space**   | O(1)            | In-place sorting                 |
| **Stable**  | ❌ No            | Swaps may reorder equal elements |


---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// To heapify a subtree rooted at index i
void heapify(vector<int>& arr, int n, int i) {
    int largest = i;       // root index
    int left = 2 * i + 1;  // left child
    int right = 2 * i + 2; // right child

    // find largest among root, left, and right
    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    // if root is not largest, swap and continue heapifying
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Step 1: Build max heap
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // Step 2: Extract elements from heap one by one
    for (int i = n - 1; i >= 0; i--) {
        swap(arr[0], arr[i]);     // move current root to end
        heapify(arr, i, 0);       // heapify reduced heap
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};

    cout << "Before sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    heapSort(arr);

    cout << "After sorting: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    return 0;
}
