# Sudoku Solver (Backtracking Approach)

## Problem Statement
You are given a partially filled **9x9 Sudoku board**.  
Each empty cell is represented by `0`.  

The task is to fill all the empty cells such that:  
1. Each **row** contains digits from `1 to 9` without repetition.  
2. Each **column** contains digits from `1 to 9` without repetition.  
3. Each of the nine **3x3 sub-boxes** of the grid contains digits from `1 to 9` without repetition.  

Write a function to solve the Sudoku puzzle and print the solved board.

---

## Approach
- Use **backtracking** to fill empty cells (`0`).  
- For each empty cell:
  - Try placing digits `1 to 9`.  
  - Check if placing the digit is **safe** (row, column, and subgrid check).  
  - If safe, place it and **recursively** solve the rest.  
  - If no valid digit is found, **backtrack**.  
- Once the board is filled completely, print the solution.  

---

## C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

bool safe(int row, int col, vector<vector<int>> &Board, int val) {
    // Row, Column and 3x3 subgrid check
    for (int i = 0; i < 9; i++) {
        // Row check
        if (Board[row][i] == val) return false;
        // Column check
        if (Board[i][col] == val) return false;
        // 3x3 sub-grid check
        if (Board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == val) return false;
    }
    return true;
}

bool solve(vector<vector<int>> &Board) {
    int n = 9;

    for (int row = 0; row < n; row++) {
        for (int col = 0; col < n; col++) {
            if (Board[row][col] == 0) { // Empty cell
                for (int val = 1; val <= n; val++) {
                    if (safe(row, col, Board, val)) {
                        Board[row][col] = val;

                        if (solve(Board)) return true;
                        else Board[row][col] = 0; // Backtrack
                    }
                }
                return false; // No valid number
            }
        }
    }
    return true; // Solved
}

void solveSudoku(vector<vector<int>> &sudoku) {
    solve(sudoku);
}

void printBoard(vector<vector<int>> &Board) {
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            cout << Board[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    // Example Sudoku puzzle (0 represents empty cells)
    vector<vector<int>> sudoku = {
        {3, 0, 6, 5, 0, 8, 4, 0, 0},
        {5, 2, 0, 0, 0, 0, 0, 0, 0},
        {0, 8, 7, 0, 0, 0, 0, 3, 1},
        {0, 0, 3, 0, 0, 0, 0, 6, 8},
        {9, 0, 0, 8, 6, 3, 0, 0, 5},
        {0, 5, 0, 0, 9, 0, 6, 0, 0},
        {1, 3, 0, 0, 0, 0, 2, 5, 0},
        {0, 0, 0, 0, 0, 0, 0, 7, 4},
        {0, 0, 5, 2, 0, 6, 3, 0, 0}
    };

    cout << "Sudoku before solving:\n";
    printBoard(sudoku);

    solveSudoku(sudoku);

    cout << "\nSolved Sudoku:\n";
    printBoard(sudoku);

    return 0;
}
