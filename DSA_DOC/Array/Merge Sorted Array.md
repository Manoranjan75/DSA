## Question
You are given two integer arrays `arr1` and `arr2`, sorted in non-decreasing order, and two integers `size1` and `size2` representing their respective lengths.  

- `arr1` has a size of `size1 + size2`, where the first `size1` elements denote the elements to be merged, and the last `size2` elements are set to `0` and should be ignored.  
- Merge `arr2` into `arr1` **in-place** so that the resulting array is sorted in non-decreasing order.

**Constraints:**  
- You must merge the arrays in-place without using extra space for another array.  

---

## Example

**Input:**  

- arr1 = [1,2,3,0,0], size1 = 3
- arr2 = [4,5], size2 = 2

**Output:**
- 1 2 3 4 5

```cpp

#include <bits/stdc++.h>
using namespace std;

void mergeArray(int arr1[], int size1, int arr2[], int size2){

    int i = size1 - size2 - 1;  // last actual element in arr1
    int j = size2 - 1;          // last element of arr2
    int k = size1 - 1;          // last position of merged array

    while(i >= 0 && j >= 0){
        if(arr1[i] > arr2[j]){
            arr1[k] = arr1[i];
            i--;
        }
        else{
            arr1[k] = arr2[j];
            j--;
        }
        k--;
    }

    while(j >= 0){   // if any elements left in arr2
        arr1[k] = arr2[j];
        j--;
        k--;
    }
}

int main(){
    int arr1[5] = {1,2,3,0,0};
    int arr2[2] = {4,5};

    mergeArray(arr1, 5, arr2, 2);

    for(auto num : arr1){
        cout << num << " ";
    }

    return 0;
}

