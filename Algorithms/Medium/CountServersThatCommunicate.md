![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1267. [Count Servers That Communicate](https://leetcode.com/problems/count-servers-that-communicate)

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `grid`, N: the number of the elements in `grid[0]`)) :
```rust
impl Solution {
    pub fn count_servers(grid: Vec<Vec<i32>>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut visited: Vec<Vec<bool>> = vec![vec![false; n]; m];
        let mut result: i32 = 0;
        for index_m in 0..m {
            let mut amount: i32 = 0;
            for index_n in 0..n {
                if grid[index_m][index_n] == 1 {
                    amount += 1;
                }
            }

            if amount < 2 {
                continue;
            }
            result += amount;

            for index_n in 0..n {
                if grid[index_m][index_n] == 1 {
                    visited[index_m][index_n] = true;
                }
            }
        }

        for index_n in 0..n {
            let mut amount: i32 = 0;
            for index_m in 0..m {
                if grid[index_m][index_n] == 1 {
                    amount += 1;
                }
            }

            if amount < 2 {
                continue;
            }
            result += amount;

            for index_m in 0..m {
                if grid[index_m][index_n] == 1 && visited[index_m][index_n] {
                    result -= 1;
                }
            }
        }

        return result
    }
}
```
