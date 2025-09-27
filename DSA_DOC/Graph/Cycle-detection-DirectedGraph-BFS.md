#  Cycle Detection in Directed Graph (DFS)

---

## Time Complexity
- Building adjacency list → **O(m)** (where `m` = number of edges)  
- DFS traversal (nodes + edges) → **O(n + m)**  
 **Overall: O(n + m)**  

---

##  Space Complexity
- Adjacency list → **O(n + m)**  
- `visited` + `dfsVisited` maps → **O(n)**  
- Recursion stack (DFS depth) → **O(n)**  
 **Overall: O(n + m)**  

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Graph {
    // Adjacency list to store graph: node -> list of neighbours
    unordered_map<int, list<int>> adj;
    // Track if a node has been visited at least once
    unordered_map<int, bool> visited;
    // Track nodes in the current recursion stack
    unordered_map<int, bool> dfsVisited;

public:
    // Function to add a directed edge u -> v
    void addEdge(int u, int v) {
        adj[u].push_back(v); // directed edge
    }

    // DFS function to detect cycle
    bool dfs(int node) {
        visited[node] = true;       // mark node as visited
        dfsVisited[node] = true;    // mark node in current recursion stack

        // Explore all neighbours of this node
        for (auto neighbour : adj[node]) {
            // If neighbour is not visited, recursively DFS
            if (!visited[neighbour]) {
                if (dfs(neighbour)) 
                    return true;    // cycle found
            }
            // If neighbour is visited and is in recursion stack → cycle detected
            else if (dfsVisited[neighbour]) {
                return true;
            }
        }

        // Backtrack: remove from recursion stack before returning
        dfsVisited[node] = false;
        return false;
    }

    // Function to check if graph has a cycle
    bool isCyclic(int n) {
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                if (dfs(i)) 
                    return true;
            }
        }
        return false;
    }
};

int main() {
    int n, m;
    cout << "Enter number of nodes: ";
    cin >> n;
    cout << "Enter number of edges: ";
    cin >> m;

    Graph g;

    cout << "Enter edges (u v) for directed graph:\n";
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        g.addEdge(u, v);
    }

    if (g.isCyclic(n))
        cout << "Graph contains a cycle\n";
    else
        cout << "Graph does not contain a cycle\n";

    return 0;
}
