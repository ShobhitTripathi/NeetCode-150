
# Graph Algorithms for Coding Interviews

A comprehensive cheat sheet of graph algorithms commonly asked in interviews, including patterns and Java code snippets.

---

## 🔗 1. Graph Representation

### ✅ Adjacency List (Most Common)
```java
Map<Integer, List<Integer>> graph = new HashMap<>();
for (int[] edge : edges) {
    graph.computeIfAbsent(edge[0], k -> new ArrayList<>()).add(edge[1]);
    // For undirected graph
    // graph.get(edge[1]).add(edge[0]);
}
```

---

## 🔍 2. Traversal Algorithms

### A. DFS (Depth-First Search)

#### ✅ Recursive
```java
void dfs(int node, Set<Integer> visited, Map<Integer, List<Integer>> graph) {
    if (visited.contains(node)) return;
    visited.add(node);
    for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
        dfs(neighbor, visited, graph);
    }
}
```

#### ✅ Iterative
```java
void dfsIterative(int start, Map<Integer, List<Integer>> graph) {
    Set<Integer> visited = new HashSet<>();
    Stack<Integer> stack = new Stack<>();
    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();
        if (visited.contains(node)) continue;
        visited.add(node);

        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            stack.push(neighbor);
        }
    }
}
```

---

### B. BFS (Breadth-First Search)
```java
void bfs(int start, Map<Integer, List<Integer>> graph) {
    Queue<Integer> queue = new LinkedList<>();
    Set<Integer> visited = new HashSet<>();
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        if (visited.contains(node)) continue;
        visited.add(node);

        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            queue.offer(neighbor);
        }
    }
}
```

---

## 🔁 3. Cycle Detection

### A. Directed Graph
```java
boolean hasCycle(int node, Map<Integer, List<Integer>> graph, Set<Integer> visiting, Set<Integer> visited) {
    if (visiting.contains(node)) return true;
    if (visited.contains(node)) return false;

    visiting.add(node);
    for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
        if (hasCycle(neighbor, graph, visiting, visited)) return true;
    }
    visiting.remove(node);
    visited.add(node);
    return false;
}
```

### B. Undirected Graph
```java
boolean hasCycle(int node, int parent, Set<Integer> visited, Map<Integer, List<Integer>> graph) {
    visited.add(node);
    for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
        if (!visited.contains(neighbor)) {
            if (hasCycle(neighbor, node, visited, graph)) return true;
        } else if (neighbor != parent) {
            return true;
        }
    }
    return false;
}
```

---

## 🛣️ 4. Shortest Path Algorithms

### A. Dijkstra’s Algorithm
```java
int[] dijkstra(Map<Integer, List<int[]>> graph, int start, int n) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[start] = 0;
    PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
    pq.offer(new int[]{start, 0});

    while (!pq.isEmpty()) {
        int[] current = pq.poll();
        int node = current[0], cost = current[1];
        if (cost > dist[node]) continue;

        for (int[] neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            int next = neighbor[0], weight = neighbor[1];
            if (dist[node] + weight < dist[next]) {
                dist[next] = dist[node] + weight;
                pq.offer(new int[]{next, dist[next]});
            }
        }
    }
    return dist;
}
```

### B. BFS for Unweighted Graphs
```java
int[] shortestPath(Map<Integer, List<Integer>> graph, int start, int n) {
    int[] dist = new int[n];
    Arrays.fill(dist, -1);
    Queue<Integer> queue = new LinkedList<>();
    dist[start] = 0;
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            if (dist[neighbor] == -1) {
                dist[neighbor] = dist[node] + 1;
                queue.offer(neighbor);
            }
        }
    }
    return dist;
}
```

---

## 🌉 5. Union-Find (Disjoint Set Union)

### ✅ Basic Pattern
```java
class UnionFind {
    int[] parent;

    UnionFind(int n) {
        parent = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }

    boolean union(int a, int b) {
        int pa = find(a), pb = find(b);
        if (pa == pb) return false;
        parent[pa] = pb;
        return true;
    }
}
```

---

## 🧠 6. Topological Sorting

### ✅ Kahn’s Algorithm
```java
List<Integer> topoSort(Map<Integer, List<Integer>> graph, int n) {
    int[] indegree = new int[n];
    for (List<Integer> neighbors : graph.values()) {
        for (int neighbor : neighbors) indegree[neighbor]++;
    }

    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < n; i++) if (indegree[i] == 0) queue.offer(i);

    List<Integer> result = new ArrayList<>();
    while (!queue.isEmpty()) {
        int node = queue.poll();
        result.add(node);
        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            if (--indegree[neighbor] == 0) queue.offer(neighbor);
        }
    }
    return result.size() == n ? result : new ArrayList<>();
}
```
