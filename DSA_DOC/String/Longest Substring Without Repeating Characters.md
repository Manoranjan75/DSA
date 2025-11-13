#  Longest Substring Without Repeating Characters (C++)

---

##  Problem Statement

Given a string `s`, find the **length of the longest substring** without repeating characters.

A *substring* is a contiguous sequence of characters within a string.

---

###  Example 1
**Input:**
s = "abcabcbb"


**Output:**
3
**Explanation:**  
The longest substring without repeating characters is `"abc"` → length = 3.

---

**Explanation:**  
The longest substring without repeating characters is `"abc"` → length = 3.

---

###  Example 2
**Input:**
s = "pwwkew"


**Output:**
3

**Explanation:**  
The longest substring without repeating characters is `"wke"`.  
(Note: `"pwk"` is also valid, but not longer.)

---

##  Approach — Sliding Window + Hash Map

We use the **sliding window technique** with a **hash map (or array)** to track the most recent index of each character.

### Steps:
1. Maintain a window `[start, i]` — initially empty.
2. Use a `vector<int> last(256, -1)` to store the **last seen index** of each character (ASCII-based).
3. For each character `s[i]`:
   - If `s[i]` was seen **inside the current window**, move `start` to `last[s[i]] + 1`.
   - Update the last seen position: `last[s[i]] = i`.
   - Update `maxLen = max(maxLen, i - start + 1)`.
4. The variable `maxLen` will hold the final answer.

---

##  Code Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

int lengthOfLongestSubstring(string s) {
    vector<int> last(256, -1);  // stores last index of each character
    int start = 0, maxLen = 0;

    for (int i = 0; i < s.size(); i++) {
        char c = s[i];

        // if character was seen in the current window
        if (last[c] >= start) {
            start = last[c] + 1;   // move start right after previous occurrence
        }

        last[c] = i;                // update last seen position
        maxLen = max(maxLen, i - start + 1);
    }
    return maxLen;
}

int main() {
    string s = "pwwkew";
    cout << "Length of longest substring without repeating characters: "
         << lengthOfLongestSubstring(s) << endl;
    return 0;
}


