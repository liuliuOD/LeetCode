![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1368. [Minimum Cost To Make At Least One Valid Path In A Grid](https://leetcode.com/problems/minimum-cost-to-make-at-least-one-valid-path-in-a-grid)

### Solution :

Method 1 (Deque, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `grid`, N: the number of the elements in `grid[0]`)) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn min_cost(grid: Vec<Vec<i32>>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut dp: Vec<Vec<i32>> = vec![vec![i32::MAX; n]; m];
        dp[0][0] = 0;
        let mut queue: VecDeque<(usize, usize)> = VecDeque::from([(0, 0)]);
        while queue.len() > 0 {
            let (index_m, index_n) = queue.pop_front().unwrap();

            for (index_offset, (offset_m, offset_n)) in [(0, 1), (0, -1), (1, 0), (-1, 0)].iter().enumerate() {
                let index_m_next: usize = (index_m as i32 + offset_m) as usize;
                let index_n_next: usize = (index_n as i32 + offset_n) as usize;
                if index_m_next >= m || index_n_next >= n {
                    continue;
                }

                let mut cost: i32 = 0;
                if grid[index_m][index_n] as usize != index_offset+1 {
                    cost += 1;
                }

                if dp[index_m][index_n]+cost >= dp[index_m_next][index_n_next] {
                    continue;
                }
                dp[index_m_next][index_n_next] = dp[index_m][index_n] + cost;

                if cost == 0 {
                    queue.push_front((index_m_next, index_n_next));
                } else {
                    queue.push_back((index_m_next, index_n_next));
                }
            }
        }

        return dp[m-1][n-1]
    }
}
```
