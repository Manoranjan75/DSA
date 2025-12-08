# Square Root of a Number (Using Binary Search)

We need to compute the **integer square root** of a non-negative number `n`.  
That means:  
Return the **floor value** of √n (the greatest integer `x` such that `x*x ≤ n`).

Example:  
- `n = 10` → output = 3  
- `n = 25` → output = 5  
- `n = 1` → output = 1  
- `n = 0` → output = 0  

---

## Approach (Binary Search)

We try to find the largest integer `x` such that:

x * x ≤ n


### Steps
1. Handle small cases: if `n == 0` or `n == 1`, return `n`.
2. Perform binary search in range `[1, n]`:
   - Let `mid = (low + high) / 2`
   - If `mid * mid == n` → return `mid`  
   - If `mid * mid < n` → store `mid` in `ans`, move right (`low = mid + 1`)
   - Else → move left (`high = mid - 1`)
3. Return `ans` (the floor square root).

This method avoids overflow by using `mid <= n / mid` instead of `mid*mid <= n`.

---

## Time & Space Complexity

- **Time Complexity:** `O(log n)`  
- **Space Complexity:** `O(1)`  

---

## C++ Code (Binary Search: Integer Square Root)

```cpp
#include <bits/stdc++.h>
using namespace std;

long long squareRoot(long long n) {
    if (n == 0 || n == 1)
        return n;

    long long low = 1, high = n, ans = 0;

    while (low <= high) {
        long long mid = low + (high - low) / 2;

        if (mid <= n / mid) {  // mid*mid <= n but safer
            ans = mid;         // store the valid mid
            low = mid + 1;     // try for bigger
        } else {
            high = mid - 1;    // try for smaller
        }
    }
    return ans;
}

int main() {
    long long n;
    cin >> n;

    cout << "Square root (floor value): " << squareRoot(n) << endl;
    return 0;
}
