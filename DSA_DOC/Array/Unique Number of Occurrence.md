# Unique Number of Occurrences (C++)

## Problem Statement

Given an array of integers `arr`, determine whether **the number of occurrences of each value is unique**.

Return:

- `true` → if no two distinct numbers in the array have the same frequency  
- `false` → otherwise  

---

## Example 1

**Input:**  
`arr = [1, 2, 2, 1, 1, 3]`

Frequencies:

| Number | Count |
|--------|--------|
| 1 | 3 |
| 2 | 2 |
| 3 | 1 |

All counts `{3, 2, 1}` are unique → **true**

---

## Example 2

**Input:**  
`arr = [1, 2]`

Frequencies:

| Number | Count |
|--------|--------|
| 1 | 1 |
| 2 | 1 |

Two numbers have the same count (1) → **false**

---

## Approach

### Step 1: Count frequency of each element  
Use an `unordered_map<int,int>` to store:


### Step 2: Check if frequencies are unique  
Use an `unordered_set<int>` to store frequencies:

- If a frequency already exists in the set → duplicate frequency found → return false
- Otherwise, insert it into the set

If we finish without duplicates → return true

---

## C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool uniqueOccurrences(vector<int>& arr) {
    unordered_map<int, int> freq;  // store frequency of elements
    
    // Count occurrences
    for (int num : arr) {
        freq[num]++;
    }
    
    unordered_set<int> seen;   // to check unique frequencies
    
    // Check uniqueness
    for (auto &p : freq) {
        if (seen.count(p.second)) {
            return false;  // duplicate frequency found
        }
        seen.insert(p.second);
    }
    
    return true;
}

int main() {
    vector<int> arr = {1, 2, 2, 1, 1, 3};
    
    if (uniqueOccurrences(arr))
        cout << "true\n";
    else 
        cout << "false\n";
        
    return 0;
}
