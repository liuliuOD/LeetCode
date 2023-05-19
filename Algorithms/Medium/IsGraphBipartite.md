![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 785. [Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite)

### Solution :

Method 1 (DFS) :
```rust
impl Solution {
    pub fn is_bipartite(graph: Vec<Vec<i32>>) -> bool {
        let n = graph.len();
        let mut colored = vec![0; n];

        for node in 0..n {
            if colored[node] != 0 {
                continue;
            }

            // if colored node not equal to pass parameter color, then this node isn't bipartite
            if Self::dfs(node, 1, &graph, &mut colored) {
                return false
            }
        }

        return true
    }

    fn dfs(node: usize, color: i8, graph: &Vec<Vec<i32>>, colored: &mut Vec<i8>) -> bool {
        // if node has been colored, it's color need to equal to parameter color
        if colored[node] != 0 {
            return colored[node] != color
        }
        colored[node] = color;

        for &neighbor in graph[node].iter() {
            if Self::dfs(neighbor as usize, -color, graph, colored) {
                return true
            }
        }

        return false
    }
}
```

Method 2 (BFS) :
```rust
use std::collections::VecDeque;
impl Solution {
    pub fn is_bipartite(graph: Vec<Vec<i32>>) -> bool {
        let n = graph.len();
        let mut colored: Vec<i8> = vec![0; n];
        let mut queue: VecDeque<usize> = VecDeque::new();

        for node_primary in 0..n {
            if colored[node_primary] != 0 {
                continue;
            }
            colored[node_primary] = 1;

            queue.push_back(node_primary);
            while !queue.is_empty() {
                let node = queue.pop_front().unwrap();
                for &neighbor in graph[node].iter() {
                    let neighbor = neighbor as usize;
                    if colored[neighbor] == 0 {
                        colored[neighbor] = -colored[node];
                        queue.push_back(neighbor);
                    } else if colored[neighbor] == colored[node] {
                        return false
                    }
                }
            }
        }

        return true
    }
}
```

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        self.colored = [0] * n
        for i in range(0, n):
            if self.colored[i] == 0:
                if not self.dfs(i, graph, 1):
                    return False
        return True
    
    def dfs(self, i: int, graph: List[List[int]], color: int) -> bool:
        if self.colored[i] != 0:
            return self.colored[i] == color
        
        self.colored[i] = color
        for j in graph[i]:
            if not self.dfs(j, graph, -color):
                return False
        return True
```

Method 2 (BFS) :
```python
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        colored = [0] * n
        for current in range(n):
            if colored[current] != 0:
                continue
            colored[current] = 1

            queue = collections.deque([current])
            while queue:
                node = queue.popleft()
                for neighbor in graph[node]:
                    if colored[neighbor] == 0:
                        colored[neighbor] = -colored[node]
                        queue.append(neighbor)
                    elif colored[neighbor] == colored[node]:
                        return False
        return True
```

Method 3 (Union Find) :
```python
```
