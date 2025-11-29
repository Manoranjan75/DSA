# Array Leaders – C++

## Problem Statement

Given an array of integers, find all the **leaders** in the array.

A **leader** is an element that is **greater than or equal to all the elements to its right**.

### Example

```text
Input:  arr = [16, 17, 4, 3, 5, 2]
Output: [17, 5, 2]

Explanation:
- 2 is a leader (rightmost element is always a leader)
- 5 > 2 → leader  
- 3 < 5 → not a leader  
- 4 < 5 → not a leader  
- 17 > 5 → leader  
- 16 < 17 → not a leader

```
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> findLeaders(vector<int>& arr) {
    int n = arr.size();
    vector<int> leaders;

    int maxRight = arr[n - 1];        // Rightmost element is always a leader
    leaders.push_back(maxRight);

    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] >= maxRight) {
            leaders.push_back(arr[i]);
            maxRight = arr[i];
        }
    }

    reverse(leaders.begin(), leaders.end());  // Reverse to maintain original order
    return leaders;
}

int main() {
    vector<int> arr = {16, 17, 4, 3, 5, 2};

    vector<int> result = findLeaders(arr);

    cout << "Leaders: ";
    for (int x : result) cout << x << " ";
    cout << endl;

    return 0;
}