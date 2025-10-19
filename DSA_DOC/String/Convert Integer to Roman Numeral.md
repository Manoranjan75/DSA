#  Convert Integer to Roman Numeral (C++)

---

##  Problem Statement

Given an integer `num`, convert it into its **Roman numeral equivalent**.  
Roman numerals use specific symbols and combinations to represent numbers.

---

###  Examples

- 3 → "III"
- 58 → "LVIII"
- 1994 → "MCMXCIV"


---

## Approach

1. Create a list of **value-symbol pairs** sorted in descending order.  
2. Repeatedly subtract the **largest possible value** from `num`.  
3. Append the corresponding **Roman symbol** to the result string.  
4. Continue until `num` becomes **0**.

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

string intToRoman(int num) {
    vector<pair<int, string>> values = {
        {1000, "M"}, {900, "CM"}, {500, "D"}, {400, "CD"},
        {100, "C"},  {90, "XC"},  {50, "L"},  {40, "XL"},
        {10, "X"},   {9, "IX"},   {5, "V"},   {4, "IV"}, {1, "I"}
    };

    string result = "";
    for (auto &val : values) {
        while (num >= val.first) {
            result += val.second;
            num -= val.first;
        }
    }
    return result;
}

int main() {
    int num;
    cout << "Enter an integer: ";
    cin >> num;

    cout << "Roman numeral: " << intToRoman(num) << endl;
    return 0;
}
