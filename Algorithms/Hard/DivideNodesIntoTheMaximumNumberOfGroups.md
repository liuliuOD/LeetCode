![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2493. [Divide Nodes Into The Maximum Number Of Groups](https://leetcode.com/problems/divide-nodes-into-the-maximum-number-of-groups)

### Solution :

Method 1 (BFS, Time Complexity: $O(N*(M+N))$, Space Complexity: $O(M+N)$ (M: the number of the elements in `edges`, N: the value of `n`)) :
```rust
use std::collections::VecDeque;

#[derive(Clone)]
#[derive(PartialEq)]
enum COLOR {
    EMPTY,
    A,
    B
}

impl Solution {
    pub fn magnificent_sets(n: i32, edges: Vec<Vec<i32>>) -> i32 {
        let n: usize = n as usize;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n+1];
        for edge in edges {
            graph[edge[0] as usize].push(edge[1] as usize);
            graph[edge[1] as usize].push(edge[0] as usize);
        }

        let mut colors: Vec<COLOR> = vec![COLOR::EMPTY; n+1];
        for node in 1..=n {
            if colors[node] != COLOR::EMPTY {
                continue;
            }
            colors[node] = COLOR::A;

            if !Self::is_bipartite(node, &mut colors, &graph) {
                return -1
            }
        }

        let mut distances: Vec<i32> = vec![0; n+1];
        for node in 1..=n {
            distances[node] = Self::longest_shortest_distance(node, &graph);
        }

        let mut result: i32 = 0;
        let mut visited: Vec<bool> = vec![false; n+1];
        for node in 1..=n {
            if visited[node] {
                continue;
            }

            result += Self::calculate_groups(node, &mut visited, &graph, &distances);
        }

        return result
    }

    fn is_bipartite(node: usize, colors: &mut Vec<COLOR>, graph: &Vec<Vec<usize>>) -> bool {
        for &node_next in &graph[node] {
            if colors[node_next] != COLOR::EMPTY {
                if colors[node] == colors[node_next] {
                    return false
                }

                continue;
            }

            colors[node_next] = match colors[node] {
                COLOR::A => COLOR::B,
                _ => COLOR::A,
            };

            if !Self::is_bipartite(node_next, colors, graph) {
                return false
            }
        }

        return true
    }

    fn longest_shortest_distance(node: usize, graph: &Vec<Vec<usize>>) -> i32 {
        let n: usize = graph.len();
        let mut visited: Vec<bool> = vec![false; n];
        visited[node] = true;
        let mut queue: VecDeque<usize> = VecDeque::from([node]);
        let mut distance: i32 = 0;
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let node_current: usize = queue.pop_front().unwrap();

                for &node_next in &graph[node_current] {
                    if visited[node_next] {
                        continue;
                    }
                    visited[node_next] = true;

                    queue.push_back(node_next);
                }
            }

            distance += 1;
        }

        return distance
    }

    fn calculate_groups(node: usize, visited: &mut Vec<bool>, graph: &Vec<Vec<usize>>, distances: &Vec<i32>) -> i32 {
        let mut result: i32 = distances[node];
        visited[node] = true;
        for &node_next in &graph[node] {
            if visited[node_next] {
                continue;
            }

            result = i32::max(result, Self::calculate_groups(node_next, visited, graph, distances));
        }

        return result
    }
}
```
