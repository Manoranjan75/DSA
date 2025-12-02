## Problem Statement

Two strings **s1** and **s2** of equal length are said to be **K-Anagrams** if:

- They can be made anagrams of each other  
- By changing **at most K characters** in *one* of the strings  

Example:  
`s1 = "anagram"`, `s2 = "grammar"`, `k = 3` → they are K-anagrams.

---

## Approach (Using Frequency Map)

### Key Idea  
If two strings are to be anagrams of each other, they must have **the same frequency of every character**.

But since we are allowed **up to K changes**, instead of matching exact frequencies:

1. Create a **frequency map for s1**:  
   Count occurrences of each character.

2. Traverse **s2**:
   - For each character in s2:  
     - If the character exists in s1’s map, reduce its count (because it's already matched).  
     - Otherwise, this character in s2 must be changed → increase `changes_needed`.

3. Finally:
   - If `changes_needed <= k`, then the strings are **K-Anagrams**  
   - Else, they are **not**


---

##  Time & Space Complexity

### Time Complexity  
- Building frequency map: **O(n)**  
- Traversing second string: **O(n)**  
➡ **Total = O(n)**

### Space Complexity  
- Frequency map: **O(1)** (fixed size, only 26 lowercase chars or 256 ASCII)  
➡ **O(1)** auxiliary space

---

##  C++ Code (Using Frequency Map Approach)

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;


bool areKAnagrams(string s1, string s2, int k) {
    // Different lengths => cannot be K-Anagrams
    if (s1.length() != s2.length())
        return false;

    unordered_map<char, int> freq;

    // Step 1: Frequency map of s1
    for (char c : s1)
        freq[c]++;

    int changesNeeded = 0;

    // Step 2: Compare with s2
    for (char c : s2) {
        if (freq[c] > 0) {
            // Match found: reduce frequency
            freq[c]--;
        } else {
            // No match: need to change this character
            changesNeeded++;
        }
    }

    // Step 3: Check the allowed K changes
    return (changesNeeded <= k);
}

int main() {
    string s1, s2;
    int k;
    cin >> s1 >> s2 >> k;

    if (areKAnagrams(s1, s2, k))
        cout << "Yes, they are K-Anagrams\n";
    else
        cout << "No, they are not K-Anagrams\n";

    return 0;
}

