![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1857. [Largest Color Value In A Directed Graph](https://leetcode.com/problems/largest-color-value-in-a-directed-graph)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(M+N)$, Space Complexity: $O(M+N)$ (M: the number of elements in `colors`, N: the number of elements in `edges`)) :
```rust
use std::collections::{VecDeque, HashMap};

impl Solution {
    pub fn largest_path_value(colors: String, edges: Vec<Vec<i32>>) -> i32 {
        let n = colors.len();
        let colors = colors.as_bytes();
        // Build adjacency list and in-degree array
        let mut adj: HashMap<i32, Vec<i32>> = HashMap::new();
        let mut in_degree = vec![0; n];
        for edge in edges {
            let a = edge[0] as usize;
            let b = edge[1] as usize;
            adj.entry(a as i32).or_insert(vec![]).push(b as i32);
            in_degree[b] += 1;
        }

        // DP table: dp[i][c] = max frequency of color c at node i
        let mut dp = vec![vec![0; 26]; n];
        let mut queue = VecDeque::new();
        let mut count = 0;
        let mut max_value = 0;

        // Initialize nodes with no incoming edges
        for i in 0..n {
            if in_degree[i] == 0 {
                queue.push_back(i as i32);
                let color = (colors[i] - b'a') as usize;
                dp[i][color] = 1;
            }
        }

        // Topological sort
        while let Some(curr) = queue.pop_front() {
            count += 1;
            let curr = curr as usize;
            // Update max_value
            max_value = max_value.max(*dp[curr].iter().max().unwrap_or(&0));

            // Process neighbors
            if let Some(neighbors) = adj.get(&(curr as i32)) {
                for &neighbor in neighbors {
                    let neighbor = neighbor as usize;
                    in_degree[neighbor] -= 1;
                    // Update color frequencies
                    for c in 0..26 {
                        let add = if c == (colors[neighbor] - b'a') as usize { 1 } else { 0 };
                        dp[neighbor][c] = dp[neighbor][c].max(dp[curr][c] + add);
                    }
                    if in_degree[neighbor] == 0 {
                        queue.push_back(neighbor as i32);
                    }
                }
            }
        }

        // Check for cycle
        return match count == n {
            true => max_value,
            _ => -1
        }
    }
}
```
