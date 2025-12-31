# Activity Selection Problem 

You are given two arrays:
- `start[]` → start times of activities  
- `finish[]` → finish times of activities  

Each activity can be performed by only one person at a time.  
Your task is to **select the maximum number of non-overlapping activities** such that:
- An activity can be selected only if its **start time is strictly greater than** the finish time of the previously selected activity.

---

## Greedy Strategy (Key Idea)

The optimal strategy is:
> **Always select the activity that finishes earliest.**

Why this works:
- Choosing the activity with the earliest finish time leaves the **maximum room for remaining activities**.
- This greedy choice guarantees the maximum number of activities.

---

## Algorithm Steps

1. Combine start and finish times into a single structure:
(finish_time, start_time)

2. Sort all activities by **finish time**.
3. Select the first activity (earliest finish).
4. For each remaining activity:
- If `start_time > last_finish_time`, select it.
5. Count the selected activities.

---

## Time & Space Complexity

- **Time Complexity:** `O(n log n)` (sorting)
- **Space Complexity:** `O(n)` (auxiliary storage for activities)

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
 int activitySelection(vector<int>& start, vector<int>& finish) {
     int n = start.size();

     vector<pair<int, int>> activities;
     for (int i = 0; i < n; i++) {
         activities.push_back({finish[i], start[i]});
     }

     // Sort activities by finish time
     sort(activities.begin(), activities.end());

     int count = 1;                 // First activity selected
     int lastFinish = activities[0].first;

     for (int i = 1; i < n; i++) {
         if (activities[i].second > lastFinish) {
             count++;
             lastFinish = activities[i].first;
         }
     }

     return count;
 }
};

int main() {
 Solution obj;

 vector<int> start  = {1, 3, 0, 5, 8, 5};
 vector<int> finish = {2, 4, 6, 7, 9, 9};

 cout << obj.activitySelection(start, finish) << endl;

 return 0;
}
