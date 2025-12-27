# Celebrity Problem

In a party of `n` people, a **celebrity** is defined as someone who:

1. **Is known by everyone else**, and  
2. **Does not know anyone else** (except themselves).

You are given a matrix `mat` of size `n x n` where:
- `mat[i][j] = 1` means person `i` knows person `j`
- `mat[i][j] = 0` means person `i` does not know person `j`
- `mat[i][i] = 1` for all `i`

Your task is to find the **index of the celebrity**, or return `-1` if no celebrity exists.

---

## Approach (Stack Elimination Method)

### Key Idea  
We eliminate **non-celebrity candidates** pairwise using a stack.

### Steps

1. Push all people (`0` to `n-1`) onto a stack.
2. While more than one person remains:
   - Pop two people `a` and `b`.
   - If `a` knows `b`, then `a` cannot be a celebrity → push `b`.
   - Else, `b` cannot be a celebrity → push `a`.
3. After elimination, one **candidate** remains.
4. Verify the candidate:
   - Candidate’s row must have all `0`s (except diagonal).
   - Candidate’s column must have all `1`s (except diagonal).

---

## Why This Works

- Every comparison eliminates **one person**.
- Stack ensures `O(n)` elimination.
- Final verification ensures correctness.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`  
  - Stack elimination: `O(n)`
  - Verification: `O(n)`
- **Space Complexity:** `O(n)` for stack

---

##  C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

bool compare_1(const vector<vector<int>>& mat, int a, int b){
    if(mat[a][b] == 1){
        return true;
    }
    else{
        return false;
    }
}

int celebrity(vector<vector<int>>& mat) {
    int n = mat.size();
    stack<int> st1;

    // Step 1: Push all people
    for(int i = 0; i < n; i++){
        st1.push(i);
    }

    // Step 2: Eliminate non-celebrities
    while(st1.size() > 1){
        int a = st1.top(); st1.pop();
        int b = st1.top(); st1.pop();

        if(compare_1(mat, a, b)){
            st1.push(b);
        }
        else{
            st1.push(a);
        }
    }

    // Step 3: Verify the candidate
    int candidate = st1.top();
    int row = 0;
    int col = 0;

    for(int i = 0; i < n; i++){
        if(i == candidate) continue;

        if(mat[candidate][i] == 0) row++;   // candidate knows no one
        if(mat[i][candidate] == 1) col++;   // everyone knows candidate
    }

    if(row == n - 1 && col == n - 1){
        return candidate;
    }

    return -1;
}

int main(){
    vector<vector<int>> mat = {
        {1, 1, 0},
        {0, 1, 0},
        {0, 1, 1}
    };

    cout << "The Celebrity is: " << celebrity(mat);
    return 0;
}
