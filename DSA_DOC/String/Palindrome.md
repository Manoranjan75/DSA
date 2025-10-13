# Check if a String is a Palindrome (C++)

---

##  Problem Statement

Given a string, check whether it reads the same **forwards and backwards** —  
ignoring **case** and **non-alphanumeric characters**.

A **palindrome** string is symmetric, for example:
- "madam" → ✅
- "racecar" → ✅
- "hello" → ❌

  
---

##  Approach

1. Use **two pointers**, one starting from the **left** and one from the **right**.  
2. Skip any **non-alphanumeric characters** (spaces, commas, punctuation).  
3. Compare characters **case-insensitively** using `tolower()`.  
4. If any mismatch occurs → return `false`.  
5. If all match → return `true`.

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPalindrome(string s) {
    int left = 0, right = s.size() - 1;

    while (left < right) {
        while (left < right && !isalnum(s[left])) left++;   // skip non-alphanumeric
        while (left < right && !isalnum(s[right])) right--; // skip non-alphanumeric

        if (tolower(s[left]) != tolower(s[right]))  // case-insensitive comparison
            return false;

        left++;
        right--;
    }
    return true;
}

int main() {
    string s;
    cout << "Enter a string: ";
    getline(cin, s);

    if (isPalindrome(s))
        cout << " It is a palindrome!" << endl;
    else
        cout << "Not a palindrome!" << endl;

    return 0;
}


