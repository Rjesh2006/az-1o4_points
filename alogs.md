#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

class FordFulkerson {
private:
    int V; // Number of vertices
    vector<vector<int>> graph; // Residual graph
    
    // BFS to find augmenting path
    bool bfs(int s, int t, vector<int>& parent) {
        vector<bool> visited(V, false);
        queue<int> q;
        
        q.push(s);
        visited[s] = true;
        parent[s] = -1;
        
        while (!q.empty()) {
            int u = q.front();
            q.pop();
            
            for (int v = 0; v < V; v++) {
                if (!visited[v] && graph[u][v] > 0) {
                    if (v == t) {
                        parent[v] = u;
                        return true;
                    }
                    q.push(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }
        return false;
    }

public:
    FordFulkerson(int vertices) : V(vertices) {
        graph.resize(V, vector<int>(V, 0));
    }
    
    // Add edge with capacity
    void addEdge(int u, int v, int capacity) {
        graph[u][v] = capacity;
    }
    
    // Main algorithm
    int maxFlow(int s, int t) {
        vector<int> parent(V);
        int max_flow = 0;
        
        // While there's an augmenting path
        while (bfs(s, t, parent)) {
            int path_flow = INT_MAX;
            
            // Find minimum capacity in the path
            for (int v = t; v != s; v = parent[v]) {
                int u = parent[v];
                path_flow = min(path_flow, graph[u][v]);
            }
            
            // Update residual capacities
            for (int v = t; v != s; v = parent[v]) {
                int u = parent[v];
                graph[u][v] -= path_flow;  // Reduce forward capacity
                graph[v][u] += path_flow;  // Increase backward capacity
            }
            
            max_flow += path_flow;
        }
        
        return max_flow;
    }
};

// Example usage
int main() {
    // Create graph with 6 vertices
    FordFulkerson ff(6);
    
    // Add edges (from, to, capacity)
    ff.addEdge(0, 1, 16); // S -> A
    ff.addEdge(0, 2, 13); // S -> B
    ff.addEdge(1, 2, 10); // A -> B
    ff.addEdge(1, 3, 12); // A -> C
    ff.addEdge(2, 1, 4);  // B -> A
    ff.addEdge(2, 4, 14); // B -> D
    ff.addEdge(3, 2, 9);  // C -> B
    ff.addEdge(3, 5, 20); // C -> T
    ff.addEdge(4, 3, 7);  // D -> C
    ff.addEdge(4, 5, 4);  // D -> T
    
    int source = 0, sink = 5;
    cout << "Maximum Flow: " << ff.maxFlow(source, sink) << endl;
    
    return 0;
}
