# KMP Pattern Matching 

The **KMP (Knuth–Morris–Pratt)** algorithm improves over the naive approach by **not re-checking characters** that are already known to match. It does this using an auxiliary array called **LPS (Longest Proper Prefix which is also Suffix)**.

---

## Idea / Approach

1. **Preprocess the pattern** to build the `lps[]` array:
   - `lps[i]` = length of the longest proper prefix of `pattern[0..i]`  
     which is also a suffix of `pattern[0..i]`.
   - This tells us **where to resume** comparison from in the pattern when a mismatch happens.

2. **Search using KMP**:
   - Use two indices:
     - `i` for text (T)
     - `j` for pattern (P)
   - If `T[i] == P[j]`, move both `i++` and `j++`.
   - If `j` reaches `m` (pattern length), we found a match ending at `i-1`.
     - Store the starting index `i - j`.
     - Then set `j = lps[j - 1]` to continue searching for next match.
   - On mismatch:
     - If `j > 0`, set `j = lps[j - 1]` (no need to move `i` back).
     - Else (`j == 0`), just move `i++`.

---

## Time & Space Complexity

- **Preprocessing (LPS):** `O(m)` where `m = pattern length`
- **Searching:** `O(n)` where `n = text length`
- **Overall:** `O(n + m)`

- **Space Complexity:** `O(m)` for the `lps` array

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Build LPS (Longest Proper Prefix which is also Suffix) array
// lps[i] = length of longest proper prefix of pat[0..i] which is also suffix of pat[0..i]
void computeLPS(const string &pat, vector<int> &lps) {
    int m = pat.size();
    lps.assign(m, 0);

    int len = 0; // length of the previous longest prefix suffix
    int i = 1;

    while (i < m) {
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1]; // try shorter prefix
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// KMP search: returns starting indices of all matches of pat in txt
vector<int> KMPsearch(const string &txt, const string &pat) {
    int n = txt.size();
    int m = pat.size();
    vector<int> lps;
    computeLPS(pat, lps);

    vector<int> result; // to store all starting indices of matches
    int i = 0; // index for txt
    int j = 0; // index for pat

    while (i < n) {
        if (txt[i] == pat[j]) {
            i++;
            j++;
        }

        if (j == m) {
            // found a match ending at i-1
            result.push_back(i - j);
            j = lps[j - 1]; // look for next match
        } else if (i < n && txt[i] != pat[j]) {
            // mismatch after j > 0 matches
            if (j != 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
    }

    return result;
}

int main() {
    string text, pattern;
    // Example input format: first line = text, second line = pattern
    getline(cin, text);
    getline(cin, pattern);

    vector<int> matches = KMPsearch(text, pattern);

    if (matches.empty()) {
        cout << "No match found\n";
    } else {
        cout << "Pattern found at indices: ";
        for (int idx : matches)
            cout << idx << " ";
        cout << "\n";
    }

    return 0;
}
