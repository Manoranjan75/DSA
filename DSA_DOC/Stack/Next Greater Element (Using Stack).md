#  Next Greater Element (Using Stack) — C++

---

##  Problem Statement

Given an array `arr[]` of size `n`, for each element, find the **Next Greater Element (NGE)** —  
the first element **to the right** that is **strictly greater** than the current one.

If no such element exists, return **-1** for that position.

---
| Operation | Complexity | Explanation                                    |
| --------- | ---------- | ---------------------------------------------- |
| **Time**  | O(n)       | Each element is pushed and popped at most once |
| **Space** | O(n)       | Stack + result array                           |


---
⚙️ Approach

We use a stack to find the next greater element efficiently.

## Steps:

### Traverse the array from right to left.

### For each element:

- Pop elements from the stack smaller or equal to the current one (since they can’t be NGE).

- If the stack is not empty, the top is the next greater element.

- Push the current element onto the stack.

- If the stack is empty → no greater element exists → store -1.

- This ensures each element is pushed and popped at most once.

---

##  Example

### Input:
```cpp
arr = [4, 5, 2, 25]

#include <bits/stdc++.h>
using namespace std;

vector<int> nextGreaterElements(vector<int>& arr) {
    int n = arr.size();
    vector<int> ans(n, -1);
    stack<int> st;

    for (int i = n - 1; i >= 0; i--) {
        // Pop smaller or equal elements
        while (!st.empty() && st.top() <= arr[i]) {
            st.pop();
        }

        // If stack not empty, top is next greater
        if (!st.empty()) {
            ans[i] = st.top();
        }

        // Push current element
        st.push(arr[i]);
    }
    return ans;
}

int main() {
    vector<int> arr = {4, 5, 2, 25};

    vector<int> result = nextGreaterElements(arr);

    cout << "Next Greater Elements: ";
    for (int x : result) cout << x << " ";
    cout << endl;

    return 0;
}

