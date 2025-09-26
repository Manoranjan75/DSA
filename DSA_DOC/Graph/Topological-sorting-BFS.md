# Topological Sort using BFS (Kahn’s Algorithm)

<p align="center">
  <img src="../../Images-Doc/Topological-sort.png" alt="Topological-sort" width="400px"/>
</p>

##  Concept  
- Works only on **Directed Acyclic Graphs (DAG)**.  
- Based on **in-degree** (number of incoming edges).  

### Steps:
1. Compute in-degree for all nodes.  
2. Push all nodes with in-degree = 0 into a queue.  
3. Repeatedly remove a node from queue, append to result, and reduce in-degree of its neighbors.  
4. If a neighbor’s in-degree becomes 0 → push it into queue.  

---

## Example  

### Input  
**Number of nodes:** 6  
**Number of edges:** 6  

**Edges (u → v):**  
| From (u) | To (v) |
|----------|--------|
| 5        | 0      |
| 5        | 2      |
| 4        | 0      |
| 4        | 1      |
| 2        | 3      |
| 3        | 1      |

### Output  
Topological sort using BFS: 5 4 2 0 3 1


---

##  Time Complexity  
- Initializing indegree → **O(V + E)**  
- Processing each vertex once → **O(V)**  
- Processing each edge once → **O(E)**  
 **Total = O(V + E)**  

---

##  Space Complexity  
- Adjacency list → **O(V + E)**  
- In-degree map → **O(V)**  
- Queue + result vector → **O(V)**  
 **Total = O(V + E)**  

---

##  Code  

```cpp
// Topological Sorting in Graph using BFS (Kahn's Algorithm)
// Graph must be DAG (Directed Acyclic Graph).

#include <bits/stdc++.h>
using namespace std;

class graph {
public:
    unordered_map<int, list<int>> gr;   // adjacency list

    // Add directed edge u -> v
    void edge(int u, int v) {
        gr[u].push_back(v);
    }

    // BFS-based Topological Sort (Kahn’s Algorithm)
    void bfs_sort() {
        vector<int> ans;
        unordered_map<int, int> in_degree;  // store indegree of nodes
        queue<int> qt;

        // Step 1: Initialize indegree of all nodes
        for (auto node : gr) {
            if (in_degree.find(node.first) == in_degree.end())
                in_degree[node.first] = 0;
            for (auto neighbour : node.second) {
                in_degree[neighbour]++;
            }
        }

        // Step 2: Push nodes with indegree 0 into queue
        for (auto node : in_degree) {
            if (node.second == 0)
                qt.push(node.first);
        }

        // Step 3: BFS process
        while (!qt.empty()) {
            int value = qt.front();
            qt.pop();

            ans.push_back(value);

            // Reduce indegree of neighbors
            for (auto neighbour : gr[value]) {
                in_degree[neighbour]--;
                if (in_degree[neighbour] == 0)
                    qt.push(neighbour);
            }
        }

        // Print result
        cout << "Topological sort using BFS: ";
        for (int x : ans) {
            cout << x << " ";
        }
        cout << endl;
    }
};

int main() {
    int nodes, edges;
    cout << "Enter the number of Nodes: ";
    cin >> nodes;
    cout << "Enter number of edges: ";
    cin >> edges;

    graph g;
    cout << "Enter edges (u v): ";
    for (int i = 0; i < edges; i++) {
        int u, v;
        cin >> u >> v;
        g.edge(u, v);
    }

    g.bfs_sort();
    return 0;
}
