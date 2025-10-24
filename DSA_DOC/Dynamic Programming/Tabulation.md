#  Fibonacci using Bottom-Up Dynamic Programming (Tabulation) — C++

---

##  Problem Statement

Find the **nth Fibonacci number**, where:

- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2)


Unlike recursion, this **iterative DP approach** builds the solution from the base cases upward —  
saving both **time** and **memory**.

---

##  Approach — Bottom-Up (Tabulation)

Instead of using recursion and memoization,  
we start from known base values and iteratively calculate higher Fibonacci numbers.

### Steps:
1. Initialize:
- prev2 = 0 → F(0)
- prev1 = 1 → F(1)

2. For each `i` from 2 to `n`:
- Compute: `curr = prev1 + prev2`
- Shift:
  ```
  prev2 = prev1
  prev1 = curr
  ```
3. After the loop, `prev1` holds `F(n)`.

---

## Complexity Analysis
### Type	Complexity
- Time	O(n) — computed iteratively in a single loop
- Space	O(1) — constant space (no recursion or extra array)
---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
 int n;
 cout << "Enter the number: ";
 cin >> n;

 int prev1 = 1;  // F(1)
 int prev2 = 0;  // F(0)

 for (int i = 2; i <= n; i++) {
     int curr = prev1 + prev2;
     prev2 = prev1;
     prev1 = curr;
 }

 cout << "Fibonacci sum: " << prev1;
 return 0;
}

