![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3212. [Count Submatrices With Equal Frequency Of X And Y](https://leetcode.com/problems/count-submatrices-with-equal-frequency-of-x-and-y)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: number of the elements in the `grid`, N: number of the elements in the `grid[0]`)) :
```rust
impl Solution {
    pub fn number_of_submatrices(grid: Vec<Vec<char>>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut dp: Vec<[i32; 2]> = vec![];
        let mut result: i32 = 0;
        for row in grid {
            let mut dp_current: Vec<[i32; 2]> = vec![];
            for (index, &item) in row.iter().enumerate() {
                let mut x: i32 = match item {
                    'X' => 1,
                    _ => 0,
                };
                let mut y: i32 = match item {
                    'Y' => 1,
                    _ => 0,
                };
                match dp_current.last() {
                    None => {},
                    Some([x_previous, y_previous]) => {
                        x += x_previous;
                        y += y_previous;
                    }
                };
                
                match dp.len() {
                    0 => {},
                    _ => {
                        x += dp[index][0];
                        y += dp[index][1];
                    },
                }

                if dp_current.len() > 0 && dp.len() > 0 {
                    x -= dp[index-1][0];
                    y -= dp[index-1][1];
                }

                dp_current.push([x, y]);

                if x > 0 && x == y {
                    result += 1;
                }
            }

            dp = dp_current;
        }

        return result
    }
}
```
