## Problem Statement

Two strings `s1` and `s2` are said to be **isomorphic** if the characters in `s1` can be replaced to get `s2`, such that:

- Every occurrence of a character is replaced with the **same character**.
- No two different characters map to the **same** character.
- The mapping is **one-to-one** and **consistent** across the string.

Example:

- `s1 = "egg"`, `s2 = "add"` → **Isomorphic**
  - e → a, g → d  
- `s1 = "foo"`, `s2 = "bar"` → **Not Isomorphic**
  - f → b, o → a, o → r (o maps to two different chars ➝ invalid)

---

##  Approach (Using Index / Mapping Arrays)

We need to ensure:

1. **Same pattern of repetition** in both strings.
2. **One-to-one mapping**:
   - If `s1[i]` maps to `s2[i]` at some position, the same must hold for all later positions.

### Key Idea

We maintain **two arrays**:

- `m1[256]` for characters of `s1`
- `m2[256]` for characters of `s2`

Each array stores the **last index where that character was seen**.

Algorithm:

1. If `s1.length() != s2.length()`, return `false`.
2. Initialize `m1` and `m2` with `-1` (meaning “not seen yet”).
3. For each index `i` from `0` to `n-1`:
   - Let `c1 = s1[i]`, `c2 = s2[i]`.
   - Check:
     - If `m1[c1] != m2[c2]`, then pattern is different ⇒ **not isomorphic**.
     - Why? Because the last seen positions of `c1` and `c2` should always match if mapping is consistent.
   - Set `m1[c1] = m2[c2] = i` (update last seen index).
4. If loop finishes with no mismatch → strings are **isomorphic**.

### Intuition with Example

`s1 = "paper"`, `s2 = "title"`

Indices:   0 1 2 3 4  
s1:        p a p e r  
s2:        t i t l e  

- i=0: p ↔ t, both first time ⇒ m1[p] = 0, m2[t] = 0  
- i=1: a ↔ i, both first time ⇒ m1[a] = 1, m2[i] = 1  
- i=2: p ↔ t  
  - m1[p] = 0, m2[t] = 0 → OK (same pattern position)  
- i=3: e ↔ l  
  - both first time ⇒ m1[e] = 3, m2[l] = 3  
- i=4: r ↔ e  
  - both first time ⇒ m1[r] = 4, m2[e] = 4  

No mismatch ⇒ isomorphic.

---

##  Time & Space Complexity

### Time Complexity
- We traverse the strings once → **O(n)**

### Space Complexity
- Two fixed-size arrays of size 256 (ASCII) → **O(1)** auxiliary space

---

## C++ Code

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;


bool areIsomorphic(const string &s1, const string &s2) {
    if (s1.length() != s2.length())
        return false;

    // Using 256 for all possible ASCII chars
    vector<int> m1(256, -1);
    vector<int> m2(256, -1);

    for (int i = 0; i < (int)s1.length(); ++i) {
        char c1 = s1[i];
        char c2 = s2[i];

        // If last seen positions differ, mapping breaks
        if (m1[c1] != m2[c2]) {
            return false;
        }

        // Set/update last seen index for both
        m1[c1] = m2[c2] = i;
    }

    return true;
}

int main() {
    string s1, s2;
    cin >> s1 >> s2;

    if (areIsomorphic(s1, s2))
        cout << "Yes, they are isomorphic\n";
    else
        cout << "No, they are not isomorphic\n";

    return 0;
}
