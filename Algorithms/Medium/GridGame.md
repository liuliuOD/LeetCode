![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2017. [Grid Game](https://leetcode.com/problems/grid-game)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `grid[0]`)) :
```rust
impl Solution {
    pub fn grid_game(grid: Vec<Vec<i32>>) -> i64 {
        let m: usize = 2;
        let n: usize = grid[0].len();
        let mut sum_row1: i64 = grid[0].iter().map(|&value| value as i64).sum();
        let mut sum_row2: i64 = 0;
        let mut result: i64 = i64::MAX;
        for index in 0..n {
            sum_row1 -= grid[0][index] as i64;
            result = i64::min(result, i64::max(sum_row1, sum_row2));
            sum_row2 += grid[1][index] as i64;
        }

        return result
    }
}
```
