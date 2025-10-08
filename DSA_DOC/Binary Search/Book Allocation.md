# Book Allocation Problem

##  Problem Statement
You are given an array `arr[]` of integers, where each element represents the number of pages in a book.  
There are `n` books and `m` students.  

The task is to allocate books to students such that:
- Each student gets **at least one book**.
- Each book is **allocated to exactly one student**.
- The allocation is **in contiguous order** (no skipping books).

Your goal is to **minimize the maximum number of pages** assigned to any student.

---

## Example

### Input:
- arr = [10, 20, 30, 40]
- n = 4 // Number of books
- m = 2 // Number of students


### Output:
- 60


### Explanation:
- Student 1 → Books [10, 20, 30] → Total = 60 pages  
- Student 2 → Book [40] → Total = 40 pages  

The maximum pages assigned = **60**, which is the minimum possible.

---

## ⚙️ Approach Explanation

### Intuition:
We want to divide the books among students such that the **maximum number of pages any student gets is as small as possible**.

We can use **Binary Search** on the answer (i.e., on the possible range of maximum pages).

---

### Algorithm Steps:
1. **Define the search space:**
   - Minimum possible pages (`s`) = 0  
   - Maximum possible pages (`e`) = sum of all pages (if one student gets all books)

2. **Apply Binary Search:**
   - Calculate `mid = (s + e) / 2`
   - Check if it is **possible** to allocate books such that no student gets more than `mid` pages

3. **Helper Function – `isPossible()`:**
   - Iterate through each book
   - Assign pages to the current student
   - If pages exceed `mid`, assign the next student
   - If the number of students exceeds `m`, return `false`

4. **Decision:**
   - If allocation is possible, store `mid` as a potential answer and try for a smaller maximum (`e = mid - 1`)
   - Otherwise, increase the lower bound (`s = mid + 1`)

5. **Return the minimum possible maximum pages**

---

##  Time and Space Complexity

| Complexity | Explanation |
|-------------|--------------|
| **Time** | `O(n * log(sum(arr)))` — because for each `mid`, we traverse the array once |
| **Space** | `O(1)` — no extra space used except variables |

---

##  Code (C++)

```cpp
#include <vector>
using namespace std;

bool isPossible(vector<int> arr, int n, int m, int mid) {
    int studentCount = 1;
    int pageSum = 0;
    
    for (int i = 0; i < n; i++) {
        if (pageSum + arr[i] <= mid) {
            pageSum += arr[i];
        } else {
            studentCount++;
            if (studentCount > m || arr[i] > mid) {
                return false;
            }
            pageSum = arr[i];
        }
        if (studentCount > m) {
            return false;
        }
    }
    return true;
}

int allocateBooks(vector<int> arr, int n, int m) {
    int s = 0;
    int sum = 0;
    
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    int e = sum;
    int ans = -1;
    int mid = s + (e - s) / 2;
    
    while (s <= e) {
        if (isPossible(arr, n, m, mid)) {
            ans = mid;
            e = mid - 1;
        } else {
            s = mid + 1;
        }
        mid = s + (e - s) / 2;
    }
    return ans;
}

