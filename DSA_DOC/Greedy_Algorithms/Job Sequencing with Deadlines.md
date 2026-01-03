# Job Sequencing with Deadlines 

You are given `n` jobs, where each job has:
- a **deadline** `deadline[i]`
- a **profit** `profit[i]`

Each job takes **exactly 1 unit of time**, and only **one job can be done at a time**.

Your task is to:
1. **Maximize the number of jobs done**
2. **Maximize the total profit**

Return both values.

---

## Key Greedy Insight

To maximize profit:
- **Always try to do the most profitable job first**.
- Schedule each job as **late as possible before its deadline** so that earlier slots remain available for other jobs.

This greedy choice leads to an optimal solution.

---

## Algorithm / Approach

1. Combine jobs as pairs: (profit, deadline)
2. Sort all jobs in **descending order of profit**.
3. Find the **maximum deadline** to determine the number of available time slots.
4. Create a `slot[]` array to track whether a time slot is occupied.
5. For each job (in sorted order):
  - Try to schedule it at the **latest available slot ≤ its deadline**
  - If a free slot is found:
    - Mark slot as occupied
    - Increment job count
    - Add job’s profit to total profit
6. Return: {number_of_jobs_done, total_profit}



---

## Time & Space Complexity

- **Time Complexity:** `O(n log n + n * d)`
- `n log n` for sorting jobs
- `n * d` in worst case for slot searching (`d` = max deadline)
- **Space Complexity:** `O(d)`
- Slot array of size `maxDeadline`

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
 vector<int> JobScheduling(vector<int>& deadline, vector<int>& profit) {
     int n = deadline.size();

     vector<pair<int, int>> jobs;
     for (int i = 0; i < n; i++) {
         jobs.push_back({profit[i], deadline[i]});
     }

     // Sort jobs by profit in descending order
     sort(jobs.begin(), jobs.end(), greater<>());

     int maxDeadline = 0;
     for (int d : deadline)
         maxDeadline = max(maxDeadline, d);

     // Slot array to mark occupied time slots
     vector<bool> slot(maxDeadline + 1, false);

     int jobCount = 0;
     int totalProfit = 0;

     // Schedule jobs
     for (auto &job : jobs) {
         int jobProfit = job.first;
         int jobDeadline = job.second;

         // Find latest free slot before deadline
         for (int t = jobDeadline; t >= 1; t--) {
             if (!slot[t]) {
                 slot[t] = true;
                 jobCount++;
                 totalProfit += jobProfit;
                 break;
             }
         }
     }

     return {jobCount, totalProfit};
 }
};

int main() {
 Solution obj;

 vector<int> deadline = {4, 1, 1, 1};
 vector<int> profit   = {20, 10, 40, 30};

 vector<int> result = obj.JobScheduling(deadline, profit);

 cout << "Jobs Done: " << result[0] << endl;
 cout << "Total Profit: " << result[1] << endl;

 return 0;
}
