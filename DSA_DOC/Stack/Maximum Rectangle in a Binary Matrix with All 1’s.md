# Maximum Rectangle in a Binary Matrix with All 1’s

Given a **binary matrix** consisting of `0`s and `1`s, find the **maximum area of a rectangle** that can be formed using only `1`s.

Each rectangle must be made of **contiguous rows and columns** containing only `1`s.

---

## Key Insight  

This problem is an **extension of the Largest Rectangle in Histogram** problem.

### Idea
- Treat **each row** of the matrix as the **base of a histogram**.
- For every row:
  - Accumulate heights of consecutive `1`s column-wise.
  - Compute the **largest rectangle area** in that histogram.
- The maximum among all rows is the final answer.

---

## Approach Breakdown

### Step 1: Histogram Concept
For each row:
- If `mat[i][j] == 1`, add height from the previous row:
mat[i][j] = mat[i][j] + mat[i-1][j]
- Else, reset height to `0`.

### Step 2: Largest Rectangle in Histogram
For each histogram (row):
- Find **Previous Smaller Element**
- Find **Next Smaller Element**
- Compute area using:
area = height[i] * (next[i] - prev[i] - 1)


---

## Time & Space Complexity

- **Time Complexity:** `O(n * m)`  
(each row processed using stack in linear time)
- **Space Complexity:** `O(m)`  
(stack + auxiliary arrays)

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

vector<int> nextSmaller (const vector<int> &vec){
  int n = vec.size();
  vector<int> ans(n);
  stack<int> st;
  st.push(-1);
  
  for(int i = n-1; i>= 0; i--){
      int curr = vec[i];
      while(st.top() != -1 && vec[st.top()] >= curr){
          st.pop();
      }
      ans[i] = st.top();
      st.push(i);
  }
  
  return ans;
}

vector<int> prevSmaller (const vector<int> &vec){
  int n = vec.size();
  vector<int> ans(n);
  stack<int> st;
  st.push(-1);
  
  for(int i = 0; i<n; i++){
      int curr = vec[i];
      while(st.top() != -1 && vec[st.top()] >= curr){
          st.pop();
      }
      ans[i] = st.top();
      st.push(i);
  }
  return ans;
}

int Rectangle_area (const vector<int> &vec){
  int n = vec.size();
  int area = 0;

  vector<int> prev = prevSmaller(vec);
  vector<int> next = nextSmaller(vec);

  for(int i = 0; i<n; i++){
      int height = vec[i];

      if(next[i] == -1){
          next[i] = n;
      }

      int width = next[i] - prev[i] - 1;
      int curr_area = height * width;
      area = max(curr_area, area);
  }

  return area;
}

int maxArea(vector<vector<int>> &mat) {
  int n = mat.size();
  int m = mat[0].size();

  int area = Rectangle_area(mat[0]);

  for(int i = 1; i < n; i++){
      for(int j = 0; j < m; j++){
          if(mat[i][j] != 0){
              mat[i][j] += mat[i-1][j];
          }
          else{
              mat[i][j] = 0;
          }
      }
      area = max(area, Rectangle_area(mat[i]));
  }
  return area;
}

int main(){
 vector<vector<int>> mat = {
      {0,1,1,0},
      {1,1,1,1},
      {1,1,1,1},
      {1,1,0,0}
  };
       
  cout <<"Max area of 1's: " << maxArea(mat) << endl;  

  return 0;
}

