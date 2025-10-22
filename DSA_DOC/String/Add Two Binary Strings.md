# Add Two Binary Strings (C++)

---

##  Problem Statement

Given two **binary strings** `a` and `b`, return their **sum** as a binary string.

---

##  Examples

- Input: a = "1010", b = "1011"
- Output: "10101"


---

##  Approach

This problem follows the same logic as **manual binary addition**.

### Steps:
1. Start from the **rightmost bits** of both strings.  
2. Add corresponding bits along with any **carry**.  
3. Compute:
   - `sum % 2` → gives the **current bit** to add.
   - `sum / 2` → gives the **carry** for the next position.
4. Continue until all bits and carry are processed.  
5. Reverse the resulting string to get the **final binary sum**.

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

string addBinary(string a, string b) {
    string result = "";
    int i = a.size() - 1, j = b.size() - 1, carry = 0;

    while (i >= 0 || j >= 0 || carry) {
        int sum = carry;
        if (i >= 0) sum += a[i--] - '0';
        if (j >= 0) sum += b[j--] - '0';
        result.push_back((sum % 2) + '0'); // Add bit
        carry = sum / 2;                   // Update carry
    }

    reverse(result.begin(), result.end());
    return result;
}

int main() {
    string a, b;
    cout << "Enter first binary string: ";
    cin >> a;
    cout << "Enter second binary string: ";
    cin >> b;

    cout << "Sum = " << addBinary(a, b) << endl;
    return 0;
}
