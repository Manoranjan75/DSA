# N-Queens Problem

The **N-Queens problem** is a classic backtracking problem where we need to place  
`N` queens on an `N x N` chessboard such that no two queens attack each other.  

A queen in chess can attack:
- Horizontally  
- Vertically  
- Diagonally  

The task is to **count the total number of possible distinct arrangements** of N queens  
on the board that satisfy these conditions.

---

## Approach Used in This Solution

1. Place queens column by column.  
2. Before placing a queen at a position `(x, y)`, check if it is safe:  
   - No queen should be present in the same row on the left.  
   - No queen should be present in the upper-left diagonal.  
   - No queen should be present in the lower-left diagonal.  
3. If safe, place the queen and move to the next column.  
4. If all columns are filled, we found one valid arrangement.  
5. Use backtracking to explore all possibilities and count them.  

---

## C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

bool safe(int x, int y, vector<vector<int>> &Board, int n) {
    int i, j;

    // check left row
    for (j = y; j >= 0; j--) {
        if (Board[x][j] == 1) return false;
    }

    // check upper diagonal (left-up)
    for (i = x, j = y; i >= 0 && j >= 0; i--, j--) {
        if (Board[i][j] == 1) return false;
    }

    // check lower diagonal (left-down)
    for (i = x, j = y; i < n && j >= 0; i++, j--) {
        if (Board[i][j] == 1) return false;
    }

    return true;
}

void solve(int y, vector<vector<int>> &Board, int &ans, int n) {
    // Base case
    if (y == n) {
        ans++;
        return;
    }

    for (int x = 0; x < n; x++) {
        if (safe(x, y, Board, n)) {
            Board[x][y] = 1;
            solve(y + 1, Board, ans, n);
            Board[x][y] = 0;
        }
    }
}

int solveNQueens(int n) {
    vector<vector<int>> Board(n, vector<int>(n, 0));
    int ans = 0;
    solve(0, Board, ans, n);
    return ans;
}

int main() {
    int q;
    cout << "Enter the number of Queens: ";
    cin >> q;
    cout << solveNQueens(q);
    return 0;
}
