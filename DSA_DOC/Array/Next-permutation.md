# Next Permutation (C++)

## Problem Statement

You are given an array of integers representing a permutation (all elements are unique).

Your task is to modify the array **in-place** to get the **next lexicographical permutation**.

- If such a permutation exists → transform it to the next one.
- If it does not exist (the current permutation is the largest) → transform it to the **smallest** (sorted in ascending order).

Example:

- Input:  [1, 2, 3] → Output: [1, 3, 2]  
- Input:  [3, 2, 1] → Output: [1, 2, 3]  
- Input:  [1, 1, 5] → Output: [1, 5, 1]

---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void nextPermutation(vector<int> &arr) {
    int n = arr.size();
    if (n <= 1) return;

    // 1. Find the pivot index i (first index from right where arr[i] < arr[i+1])
    int i = n - 2;
    while (i >= 0 && arr[i] >= arr[i + 1]) {
        i--;
    }

    // 2. If no pivot found, the entire array is non-increasing
    if (i < 0) {
        // This is the last permutation, reverse to get the first
        reverse(arr.begin(), arr.end());
        return;
    }

    // 3. Find rightmost successor of pivot in the suffix: arr[j] > arr[i]
    int j = n - 1;
    while (arr[j] <= arr[i]) {
        j--;
    }

    // 4. Swap pivot and successor
    swap(arr[i], arr[j]);

    // 5. Reverse the suffix starting at i+1 to minimize it
    reverse(arr.begin() + i + 1, arr.end());
}

int main() {
    vector<int> arr = {1, 3, 5, 4, 2};

    cout << "Original: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    nextPermutation(arr);

    cout << "Next permutation: ";
    for (int x : arr) cout << x << " ";
    cout << endl;

    return 0;
}
