# Longest Substring With Exactly K Unique Characters

Given a string `str` and an integer `k`, find the **length** of the **longest substring** that contains **exactly `k` distinct (unique) characters**.

Example:  

- `str = "aabacbebebe"`, `k = 3`  
  Longest substring with exactly 3 unique characters has length `7` (substring `"cbebebe"`).

---

## Approach (Sliding Window + Frequency Array)

We use the **sliding window** technique with two pointers `i` and `j`:

- `i` = start of window  
- `j` = end of window  

We also maintain:

- An array `vec[26]` for character frequencies (assuming lowercase `a–z`).
- An integer `count` = number of **distinct** characters in the current window.
- An integer `window` = best (maximum) window length found so far.

### Steps

1. Initialize `i = 0`, `j = 0`, `count = 0`, `window = -1`.
2. Move `j` from `0` to `n-1`:
   - Include `str[j]` in the window:
     - Increment `vec[str[j] - 'a']`.
     - If this frequency becomes 1, increment `count` (new unique character).
3. If `count > k`:
   - Shrink from the **left** by moving `i` forward:
     - Decrease `vec[str[i] - 'a']`.
     - If frequency becomes 0, decrement `count`.
     - Increment `i`.
   - Keep shrinking until `count <= k`.
4. If `count == k`:
   - Current window `[i..j]` has exactly `k` unique characters.
   - Update `window = max(window, j - i + 1)`.
5. At the end, `window` holds the **maximum length** of a substring with exactly `k` unique characters.
   - If no such substring exists, `window` stays `-1`.

---

## Time & Space Complexity

- **Time Complexity:**  
  Each character is processed at most twice (once when `j` moves right, once when `i` moves right) → **O(n)**.

- **Space Complexity:**  
  Frequency array `vec[26]` (constant size for lowercase English letters) → **O(1)**.

---

##  Code (Using the Given Implementation)

```cpp
#include<bits/stdc++.h>
using namespace std;

int unique_k(const string & str, int k){
    int n = str.size();
    int i = 0;
    int j = 0;
    int count = 0;
    int window = -1;

    vector<int> vec(26,0);

    while(j < n){

        vec[str[j] - 'a']++;

        if(vec[str[j] - 'a'] == 1) 
            count++;

        while(count > k){
            vec[str[i] - 'a']--;

            if(vec[str[i] - 'a'] == 0) 
                count--;

            i++;
        }

        if(count == k){
            window = max(window, j - i + 1);
        }

        j++;
    }

    return window;
}

int main(){
    string str1 = "aabacbebebe";
    int k = 3;

    int ans = unique_k(str1, k);
    cout << "Longest K Unique Characters Substring Length: " << ans;

    return 0;
}
