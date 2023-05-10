![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Make Costs Of Paths Equal In A Binary Tree](https://leetcode.com/problems/make-costs-of-paths-equal-in-a-binary-tree)

### Solution :

Method 1 (DFS, balance subtree) :
```rust
use std::cmp;
impl Solution {
    pub fn min_increments(n: i32, cost: Vec<i32>) -> i32 {
        let mut result = 0;
        Self::dfs(0, &cost, &mut result);

        result
    }

    fn dfs(index: usize, cost: &Vec<i32>, result: &mut i32) -> i32 {
        if index >= cost.len() {
            return 0
        }

        let node_left = Self::dfs((index + 1) * 2 - 1, cost, result);
        let node_right = Self::dfs((index + 1) * 2, cost, result);

        *result += (node_left - node_right).abs();

        return cost[index] + cmp::max(node_left, node_right)
    }
}
```
