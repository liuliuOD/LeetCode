![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2642. [Design Graph With Shortest Path Calculator](https://leetcode.com/problems/design-graph-with-shortest-path-calculator)

### Solution :

Method 1 (Dijkstra) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
struct Graph {
    n: usize,
    graph: Vec<Vec<(i32, usize)>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl Graph {

    fn new(n: i32, edges: Vec<Vec<i32>>) -> Self {
        let n = n as usize;
        let mut graph = vec![vec![]; n];
        for edge in edges {
            graph[edge[0] as usize].push((edge[2], edge[1] as usize));
        }

        Self {
            n: n,
            graph: graph,
        }
    }
    
    fn add_edge(&mut self, edge: Vec<i32>) {
        self.graph[edge[0] as usize].push((edge[2], edge[1] as usize));
    }
    
    fn shortest_path(&self, node1: i32, node2: i32) -> i32 {
        let mut weights = vec![i32::MAX; self.n];
        weights[node1 as usize] = 0;
        let mut heap = BinaryHeap::from([(Reverse(0), node1 as usize)]);
        while !heap.is_empty() {
            let (Reverse(weight), point_start) = heap.pop().unwrap();

            for &(weight_target, point_target) in self.graph[point_start].iter() {
                let weight_start_to_target = weight_target + weight;

                if weights[point_target] > weight_start_to_target {
                    weights[point_target] = weight_start_to_target;

                    heap.push((Reverse(weight_start_to_target), point_target));
                }
            }
        }

        match weights[node2 as usize] {
            i32::MAX => -1,
            value => value,
        }
    }
}
```

Method 2 (BFS) :
```rust
use std::collections::VecDeque;
struct Graph {
    n: usize,
    graph: Vec<Vec<(i32, usize)>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl Graph {

    fn new(n: i32, edges: Vec<Vec<i32>>) -> Self {
        let n = n as usize;
        let mut graph = vec![vec![]; n];
        for edge in edges {
            graph[edge[0] as usize].push((edge[2], edge[1] as usize));
        }

        Self {
            n: n,
            graph: graph,
        }
    }
    
    fn add_edge(&mut self, edge: Vec<i32>) {
        self.graph[edge[0] as usize].push((edge[2], edge[1] as usize));
    }
    
    fn shortest_path(&self, node1: i32, node2: i32) -> i32 {
        let mut weights = vec![i32::MAX; self.n];
        weights[node1 as usize] = 0;
        let mut queue = VecDeque::from([(0, node1 as usize)]);
        while !queue.is_empty() {
            let (weight, point_start) = queue.pop_front().unwrap();

            for &(weight_target, point_target) in self.graph[point_start].iter() {
                let weight_start_to_target = weight_target + weight;

                if weights[point_target] > weight_start_to_target {
                    weights[point_target] = weight_start_to_target;

                    queue.push_back((weight_start_to_target, point_target));
                }
            }
        }

        match weights[node2 as usize] {
            i32::MAX => -1,
            value => value,
        }
    }
}
```

### Solution :

```python
# Your Graph object will be instantiated and called as such:
# obj = Graph(n, edges)
# obj.addEdge(edge)
# param_2 = obj.shortestPath(node1,node2)
```

Method 1 (BFS):
```python
class Graph:

    def __init__(self, n: int, edges: List[List[int]]):
        self.graph = [[] for _ in range(n)]
        for node_from, node_to, cost in edges:
            self.graph[node_from].append((cost, node_to))

    def addEdge(self, edge: List[int]) -> None:
        self.graph[edge[0]].append((edge[2], edge[1]))

    def shortestPath(self, node1: int, node2: int) -> int:
        costs = [inf] * len(self.graph)
        costs[node1] = 0

        queue = deque([(0, node1)])
        while queue:
            cost, node_current = queue.popleft()

            for cost_next, node_next in self.graph[node_current]:
                cost_total = cost + cost_next
                if cost_total >= costs[node_next]:
                    continue
                costs[node_next] = cost_total

                queue.append((cost+cost_next, node_next))

        return -1 if costs[node2] is inf else costs[node2]
```

Method 2 (Dijkstra) :
```python
class Graph:

    def __init__(self, n: int, edges: List[List[int]]):
        self.graph = [[] for _ in range(n)]
        for node_from, node_to, cost in edges:
            self.graph[node_from].append((cost, node_to))

    def addEdge(self, edge: List[int]) -> None:
        self.graph[edge[0]].append((edge[2], edge[1]))

    def shortestPath(self, node1: int, node2: int) -> int:
        costs = [inf] * len(self.graph)
        costs[node1] = 0

        heap = [(0, node1)]
        while heap:
            cost, node_current = heapq.heappop(heap)
            if node_current == node2:
                return cost
            """
            # Option 1

            if cost > costs[node_current]:
                continue
            """

            for cost_next, node_next in self.graph[node_current]:
                cost_total = cost + cost_next
                if cost_total >= costs[node_next]:
                    continue
                costs[node_next] = cost_total

                heapq.heappush(heap, (cost+cost_next, node_next))

        return -1
```

Method 3 (Floyd Warshall) :
```python
class Graph:

    def __init__(self, n: int, edges: List[List[int]]):
        # Option 1
        self.costs = [[inf]*n for _ in range(n)]
        for index in range(n):
            self.costs[index][index] = 0
        """
        # Option 2

        self.costs = [[inf]*index + [0] + [inf]*(n-index-1) for index in range(n)]
        """

        for node_from, node_to, cost in edges:
            self.costs[node_from][node_to] = cost

        """
        i: start, j: target, k: intermediate
        """
        for k in range(n):
            for i in range(n):
                for j in range(n):
                    self.costs[i][j] = min(
                        self.costs[i][j],
                        self.costs[i][k]+self.costs[k][j]
                    )

    def addEdge(self, edge: List[int]) -> None:
        node_from, node_to, cost = edge
        n = len(self.costs)
        for i in range(n):
            for j in range(n):
                self.costs[i][j] = min(self.costs[i][j], self.costs[i][node_from]+self.costs[node_to][j]+cost)

    def shortestPath(self, node1: int, node2: int) -> int:
        return -1 if self.costs[node1][node2] is inf else self.costs[node1][node2]
```
