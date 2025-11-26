# Happy Number (C++)

## Problem Statement

A **happy number** is defined as follows:

- Start with any positive integer `n`.
- Replace the number by the **sum of the squares of its digits**.
- Repeat the process until:
  - The number becomes `1` (then it is a happy number), or
  - It loops endlessly in a cycle that does **not** include `1` (then it is not a happy number).

Your task:  
Given an integer `n`, determine whether it is a **happy number**.

---

## Examples

### Example 1

```text
Input:  n = 19
Output: true


Explanation:

1² + 9² = 1 + 81 = 82

8² + 2² = 64 + 4 = 68

6² + 8² = 36 + 64 = 100

1² + 0² + 0² = 1

```

## Time & Space Complexity:
- Time: O(n)
- Space: O(n)
```cp
#include <bits/stdc++.h>
using namespace std;

// Helper function to compute sum of squares of digits of n
int getNext(int n) {
    int sum = 0;
    while (n > 0) {
        int digit = n % 10;
        sum += digit * digit;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    unordered_set<int> seen;

    while (n != 1 && !seen.count(n)) {
        seen.insert(n);
        n = getNext(n);
    }

    return (n == 1);
}

int main() {
    int n;
    cout << "Enter a number: ";
    cin >> n;

    if (isHappy(n))
        cout << n << " is a Happy Number\n";
    else
        cout << n << " is NOT a Happy Number\n";

    return 0;
}
