![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2467. [Most Profitable Path In A Tree](https://leetcode.com/problems/most-profitable-path-in-a-tree)

### Solution :

Method 1 (DFS + BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `edges`)) :
```rust
use std::collections::{HashMap, VecDeque};

impl Solution {
    pub fn most_profitable_path(edges: Vec<Vec<i32>>, bob: i32, amount: Vec<i32>) -> i32 {
        let n: usize = edges.len() + 1;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for edge in edges {
            graph[edge[0] as usize].push(edge[1] as usize);
            graph[edge[1] as usize].push(edge[0] as usize);
        }

        let mut path_bob: HashMap<usize, usize> = HashMap::new();
        Self::traverse_bob(bob as usize, 0, &mut path_bob, &graph);

        let mut result: i32 = i32::MIN;
        let mut visited: Vec<bool> = vec![false; n];
        let mut queue: VecDeque<(usize, usize, i32)> = VecDeque::from([(0, 0, 0)]);
        while queue.len() > 0 {
            let (current, amount_previous, profit) = queue.pop_front().unwrap();
            let mut profit_all: i32 = profit;
            visited[current] = true;

            if path_bob.contains_key(&current) && *path_bob.get(&current).unwrap() == amount_previous {
                profit_all += amount[current] / 2;
            } else if !path_bob.contains_key(&current) || amount_previous < *path_bob.get(&current).unwrap() {
                profit_all += amount[current];
            }

            if current != 0 && graph[current].len() == 1 {
                result = i32::max(result, profit_all);
            }

            for &next in &graph[current] {
                if visited[next] {
                    continue;
                }

                queue.push_back((next, amount_previous+1, profit_all));
            }
        }

        return result
    }

    fn traverse_bob(current: usize, amount: usize, path_bob: &mut HashMap<usize, usize>, graph: &Vec<Vec<usize>>) -> bool {
        if path_bob.contains_key(&current) {
            return false
        }
        path_bob.insert(current, amount);
        if path_bob.contains_key(&0) {
            return true
        }

        for &next in &graph[current] {
            if Self::traverse_bob(next, amount+1, path_bob, graph) {
                return true
            }
        }

        path_bob.remove(&current);
        return false
    }
}
```
