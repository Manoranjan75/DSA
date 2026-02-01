# Trie Data Structure — Insert & Search  

<p align="center">
  <img src="../../Images-Doc/Trie.png" alt="Trie" width="400px"/>
</p>


A **Trie** (Prefix Tree) is a special tree used to store strings efficiently, especially for prefix-based operations such as:
- Autocomplete  
- Searching words  
- Spell checking  
- Prefix queries  
- Dictionary lookup  

---

#  Trie Node Structure

Each node stores:
- `char data`  
- `TrieNode* children[26]` → One pointer for each lowercase letter (`a–z`)  
- `bool isTerminal` → Marks end of a valid word  

---

#  Why Use a Trie?

Tries allow:
- **Fast word insert & search**
- **Efficient prefix matching**
- **No hash collisions (unlike unordered_map)**  
- **Alphabet-based branching → predictable O(L)** operations  

---

#  Insert Operation — Idea

Inserting `"apple"`:
1. Start from root  
2. For each character:
   - If child exists → follow
   - Else → create a new node
3. At the end, mark isTerminal = true  

 Time = O(L)  
 Space = O(L) (new nodes created only when needed)

---

#  Search Operation — Idea

Searching `"app"`:
1. Start from root  
2. Traverse using each character  
3. If at any point child is missing → return false  
4. At last character, check if node isTerminal  

 Time = O(L)  
 Space = O(1) (ignoring recursion stack)

---

# Time & Space Complexity

Let:
- **L = length of the word**
- **N = number of words inserted so far**
- **Alphabet size = 26** (constant)

###  Insert Operation  
| Metric | Complexity |
|--------|------------|
| Time   | **O(L)** |
| Space  | **O(L)** (in worst case we create new nodes) |

###  Search Operation  
| Metric | Complexity |
|--------|------------|
| Time   | **O(L)** |
| Space  | **O(1)** (or O(L) if recursive stack considered) |

###  Total Space Used by Trie  
Worst case: Number of nodes = sum of lengths of all inserted words

Space = **O(total characters inserted × alphabet size)** but since children array is fixed (26), this becomes:

**O(total characters)**

---

#  C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

class TrieNode {
public:
    char data;
    TrieNode* children[26];
    bool isTerminal;

    TrieNode(char ch) {
        data = ch;
        for (int i = 0; i < 26; i++) {
            children[i] = NULL;
        }
        isTerminal = false;
    }
};

class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode('\0');
    }

    // Insert utility
    void insertUtil(TrieNode* root, string word) {
        if (word.length() == 0) {
            root->isTerminal = true;
            return;
        }

        int index = word[0] - 'a';
        TrieNode* child;

        if (root->children[index] != NULL) {
            child = root->children[index];
        }
        else {
            child = new TrieNode(word[0]);
            root->children[index] = child;
        }

        insertUtil(child, word.substr(1));
    }

    // Insert word in Trie
    void insert(string word) {
        insertUtil(root, word);
    }

    // Search utility
    bool searchUtil(TrieNode* root, string word) {
        if (word.length() == 0) {
            return root->isTerminal;
        }

        int index = word[0] - 'a';

        if (root->children[index] == NULL) {
            return false;
        }

        return searchUtil(root->children[index], word.substr(1));
    }

    // Search word
    bool search(string word) {
        return searchUtil(root, word);
    }
};

