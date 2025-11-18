# First Non-Repeating Character in a Stream (Queue + Frequency Array)

## Problem Statement  
You are given a stream of characters (a string).  
For each character that arrives, you must determine the first non-repeating character seen so far.  
If no such character exists at that time, output a dash (`-`).

---

## Example

### Input:
a a b c


### Output:
a - b b


### Explanation:
- Stream: `a` → first non-repeating is `a`  
- Stream: `a,a` → all repeating → `-`  
- Stream: `a,a,b` → first non-repeating is `b`  
- Stream: `a,a,b,c` → still `b`

---

# Approach (Queue + Frequency Array)

To efficiently track the first non-repeating character at each step, we maintain:

### 1. A queue  
Stores characters in the order they appear.

### 2. A frequency array  
`freq[26]` stores how many times each character has appeared.

### Algorithm:
1. For each character `c` in the stream:
   - Increment `freq[c]`
   - Push `c` into the queue
2. While the queue is not empty AND the front element has frequency > 1:
   - Pop it from the queue
3. After this cleanup:
   - If the queue is empty → output `-`
   - Else → output `queue.front()`

This ensures that the queue always keeps potential candidates for the first non-repeating character.

---

# Dry Run

### Input: `"aabc"`

| Step | Stream | Queue Content      | freq changes  | Output |
|------|--------|--------------------|---------------|--------|
| 1    | a      | a                  | a = 1         | a      |
| 2    | aa     | a, a → a popped    | a = 2         | -      |
| 3    | aab    | b                  | b = 1         | b      |
| 4    | aabc   | b, c               | b = 1, c = 1  | b      |

---

# C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void firstNonRepeating(string s) {
    vector<int> freq(26, 0);   // frequency of characters
    queue<char> q;

    for (char c : s) {
        freq[c - 'a']++;       // update frequency
        q.push(c);             // push into queue

        // remove repeating characters from the front
        while (!q.empty() && freq[q.front() - 'a'] > 1) {
            q.pop();
        }

        // output result at this stage
        if (q.empty())
            cout << "- ";
        else
            cout << q.front() << " ";
    }
}

int main() {
    string s = "aabc";
    firstNonRepeating(s);
    return 0;
}
