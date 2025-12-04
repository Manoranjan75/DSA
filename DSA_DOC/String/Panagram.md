# Pangram Check 
A **pangram** is a sentence that contains all **26 English letters** at least once.  
Example:  
`The quick brown fox jumps over the lazy dog`

To check if a string is a pangram:

- Convert characters to lowercase  
- Track presence of each letter using a boolean array of size 26  
- If all are present → Pangram, else Not Pangram

### Time Complexity
`O(n)` — single pass through the string

### Space Complexity
`O(1)` — only 26 booleans

### C++ Code

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

bool isPangram(const string &s) {
    bool seen[26] = {false};

    for (char c : s) {
        if (isalpha(c)) {
            c = tolower(c);
            seen[c - 'a'] = true;
        }
    }

    for (int i = 0; i < 26; i++) {
        if (!seen[i]) return false;
    }
    return true;
}

int main() {
    string s;
    getline(cin, s);

    if (isPangram(s))
        cout << "Pangram\n";
    else
        cout << "Not Pangram\n";

    return 0;
}