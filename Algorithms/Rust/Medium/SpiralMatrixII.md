![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii)


### Solution :

Method 1 (DFS) :
```rust
impl Solution {
    pub fn generate_matrix(n: i32) -> Vec<Vec<i32>> {
        let n = n as usize;
        let mut result = vec![vec![0; n]; n];
        let mut value = 0;
        Self::dfs(0, 0, 0, &mut value, &mut result);
        result
    }

    fn dfs(i: usize, j: usize, mode: usize, value: &mut i32, result: &mut Vec<Vec<i32>>) {
        if i < 0 || j < 0 || i >= result.len() || j >= result[0].len() || result[i][j] > 0 {
            return
        }
        *value += 1;
        result[i][j] = *value;

        let moves = vec![(i, j+1),(i+1, j),(i, j-1),(i-1, j)];
        let mut mode_current = mode;
        loop {
            Self::dfs(moves[mode_current].0, moves[mode_current].1, mode_current, value, result);

            mode_current += 1;
            if mode_current == moves.len() && *value as usize != result.len() * result[0].len() {
                mode_current = 0;
            }

            if mode_current >= moves.len() {
                break;
            }
        }
    }
}
```
