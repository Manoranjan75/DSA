#  Check if Two Strings Are Anagrams (C++)

---

##  Problem Statement

Given two strings `s` and `t`, determine if they are **anagrams** of each other.  
Two strings are anagrams if they contain the **same characters** with the **same frequency**,  
but possibly in a **different order**.

---

###  Examples

- "listen" and "silent" → ✅ anagrams
- "rat" and "car" → ❌ not anagrams

  
---

## ⚙️ Approach

We use a **frequency counting method** for lowercase English letters:

1. If string lengths differ → return `false`.
2. Create a **frequency array** of size 26 (for ‘a’ to ‘z’).
3. For each character in `s`, **increment** its count.
4. For each character in `t`, **decrement** its count.
5. If all values in the array become 0 → strings are **anagrams**.

---

## ✅ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isAnagram(string s, string t) {
    if (s.length() != t.length())
        return false;

    vector<int> freq(26, 0);
    for (char c : s) freq[c - 'a']++;
    for (char c : t) freq[c - 'a']--;

    for (int count : freq)
        if (count != 0)
            return false;

    return true;
}

int main() {
    string s, t;
    cout << "Enter first string: ";
    cin >> s;
    cout << "Enter second string: ";
    cin >> t;

    if (isAnagram(s, t))
        cout << "The strings are anagrams!" << endl;
    else
        cout << " Not anagrams!" << endl;

    return 0;
}

