
## Problem Statement

Print numbers from **1 to N**, but:

- For multiples of **3**, print `"Fizz"`  
- For multiples of **5**, print `"Buzz"`  
- For multiples of **both 3 and 5**, print `"FizzBuzz"`  
- Otherwise, print the number itself  

---

## Approach

1. Loop from `1` to `N`.
2. For each number:
   - Check if divisible by both **3 and 5** → print `"FizzBuzz"`
   - Else if divisible by **3** → print `"Fizz"`
   - Else if divisible by **5** → print `"Buzz"`
   - Else print the number.
3. Use simple modulo operations.

---

## Time & Space Complexity

### Time Complexity
- Loop runs once for each number → **O(N)**

### Space Complexity
- No extra data structures used → **O(1)**

---

## C++ Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    for (int i = 1; i <= n; i++) {
        if (i % 3 == 0 && i % 5 == 0) {
            cout << "FizzBuzz\n";
        }
        else if (i % 3 == 0) {
            cout << "Fizz\n";
        }
        else if (i % 5 == 0) {
            cout << "Buzz\n";
        }
        else {
            cout << i << "\n";
        }
    }

    return 0;
}
