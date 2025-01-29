![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 684. [Redundant Connection](https://leetcode.com/problems/redundant-connection)

### Solution :

Method 1 (DFS, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `edges`)):
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_redundant_connection(edges: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = edges.len();
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n+1];
        for edge in &edges {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            graph[a].push(b);
            graph[b].push(a);
        }

        let mut result: Vec<i32> = vec![0; 2];
        for edge in edges {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            let mut visited: HashSet<usize> = HashSet::new();
            Self::dfs(a, a, b, &mut visited, &graph);
            if visited.len() == n {
                result = Vec::from([a as i32, b as i32]);
            }
        }

        return result
    }

    fn dfs(node: usize, a: usize, b: usize, visited: &mut HashSet<usize>, graph: &Vec<Vec<usize>>) {
        if visited.contains(&node) {
            return
        }
        visited.insert(node);

        for &node_next in &graph[node] {
            if node == a && node_next == b {
                continue;
            }

            Self::dfs(node_next, a, b, visited, graph);
        }
    }
}
```

Method 2 (DFS + Cycle, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `edges`)):
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_redundant_connection(edges: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = edges.len();
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n+1];
        for edge in &edges {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            graph[a].push(b);
            graph[b].push(a);
        }

        let mut cycle_start: i32 = -1;
        let mut parents: Vec<i32> = vec![-1; n+1];
        let mut visited: Vec<bool> = vec![false; n+1];
        Self::dfs(1, &mut cycle_start, &mut parents, &mut visited, &graph);

        let mut nodes_cycle: HashSet<i32> = HashSet::new();
        let mut node: i32 = cycle_start;
        loop {
            nodes_cycle.insert(node);
            node = parents[node as usize];
            if node == cycle_start {
                break;
            }
        }

        for edge in edges.into_iter().rev() {
            if nodes_cycle.contains(&edge[0]) && nodes_cycle.contains(&edge[1]) {
                return edge
            }
        }

        unreachable![];
    }

    fn dfs(node: usize, cycle_start: &mut i32, parents: &mut Vec<i32>, visited: &mut Vec<bool>, graph: &Vec<Vec<usize>>) {
        visited[node] = true;
        for &node_next in &graph[node] {
            if !visited[node_next] {
                parents[node_next] = node as i32;
                Self::dfs(node_next, cycle_start, parents, visited, graph);
            } else if *cycle_start == -1 && node_next as i32 != parents[node] {
                parents[node_next] = node as i32;
                *cycle_start = node_next as i32;
            }
        }
    }
}
```

Method 3 (BFS, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `edges`)):
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn find_redundant_connection(edges: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = edges.len();
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n+1];
        for edge in &edges {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            graph[a].push(b);
            graph[b].push(a);
        }

        /* Option 1 */
        let mut result: Vec<i32> = vec![0; 2];
        for edge in edges {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            if Self::bfs(a, b, &graph) {
                result = Vec::from([a as i32, b as i32]);
            }
        }

        return result
        /* Option 2: early return

        for edge in edges.into_iter().rev() {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            if Self::bfs(a, b, &graph) {
                return Vec::from([a as i32, b as i32])
            }
        }

        unreachable![];
        */
    }

    fn bfs(a: usize, b: usize, graph: &Vec<Vec<usize>>) -> bool {
        let n: usize = graph.len();
        let mut visited: Vec<bool> = vec![false; n];
        visited[0] = true;
        let mut queue: VecDeque<usize> = VecDeque::from([a]);
        while queue.len() > 0 {
            let node: usize = queue.pop_front().unwrap();
            if visited[node] {
                continue;
            }
            visited[node] = true;

            for &node_next in &graph[node] {
                if node == a && node_next == b {
                    continue;
                }

                queue.push_back(node_next);
            }
        }

        return visited.into_iter()
            .filter(|value| !value)
            .count() == 0
    }
}
```
