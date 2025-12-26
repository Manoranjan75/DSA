# Largest Rectangle in Histogram (Using Stack)

Given an array of integers where each value represents the **height of a histogram bar** and each bar has a width of `1`, find the **area of the largest rectangle** that can be formed inside the histogram.

---

## Core Idea

For each bar `i`, treat it as the **smallest height** of a rectangle and try to expand:
- **Left** until a smaller bar appears
- **Right** until a smaller bar appears

So for every bar, we need:
- **Previous Smaller Element index**
- **Next Smaller Element index**

Using these two, we can compute the maximum rectangle area with that bar as the limiting height.

---

## Width & Area Formula

For a bar at index `i`:
- height = vec[i]
- width = nextSmaller[i] - prevSmaller[i] - 1
- area = height * width


The maximum among all such areas is the answer.

---

## Approach (Using Stack)

### 1. Previous Smaller Element
- Traverse from **left to right**
- Maintain a stack of indices
- For each bar, pop elements until a smaller bar is found

### 2. Next Smaller Element
- Traverse from **right to left**
- Similar logic using stack

### 3. Compute Area
- If no next smaller exists, treat its index as `n`
- Use the formula to compute area for each bar

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`  
  Each element is pushed and popped at most once.

- **Space Complexity:** `O(n)`  
  For stacks and auxiliary arrays.

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> nextSmaller(const vector<int> &vec){
    int n = vec.size();
    vector<int> ans(n);
    stack<int> st;
    st.push(-1);

    for(int i = n - 1; i >= 0; i--){
        int curr = vec[i];
        while(st.top() != -1 && vec[st.top()] >= curr){
            st.pop();
        }
        ans[i] = st.top();
        st.push(i);
    }
    return ans;
}

vector<int> prevSmaller(const vector<int> &vec){
    int n = vec.size();
    vector<int> ans(n);
    stack<int> st;
    st.push(-1);

    for(int i = 0; i < n; i++){
        int curr = vec[i];
        while(st.top() != -1 && vec[st.top()] >= curr){
            st.pop();
        }
        ans[i] = st.top();
        st.push(i);
    }
    return ans;
}

int Rectangle(const vector<int> &vec){
    int n = vec.size();
    int area = 0;

    vector<int> prev = prevSmaller(vec);
    vector<int> next = nextSmaller(vec);

    for(int i = 0; i < n; i++){
        int height = vec[i];

        if(next[i] == -1){
            next[i] = n;
        }

        int width = next[i] - prev[i] - 1;
        int curr_area = height * width;
        area = max(area, curr_area);
    }

    return area;
}

int main(){
    vector<int> vec = {60, 20, 50, 40, 10, 50, 60};
    cout << "Largest rectangle in Histogram is: " << Rectangle(vec);
    return 0;
}
