![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2290. [Minimum Obstacle Removal To Reach Corner](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner)

### Solution :

Method 1 (BFS, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `grid`, N: the number of the elements in `grid[0]`)) :
```rust
use std::collections::VecDeque;

const MOVE: [(i32, i32); 4] = [
    (0, -1),
    (0, 1),
    (-1, 0),
    (1, 0),
];
impl Solution {
    pub fn minimum_obstacles(grid: Vec<Vec<i32>>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut result: Vec<Vec<i32>> = vec![vec![i32::MAX; n]; m];
        result[0][0] = 0;
        let mut queue: VecDeque<(usize, usize, i32)> = VecDeque::from([(0, 0, 0)]);
        while queue.len() > 0 {
            let item: (usize, usize, i32) = queue.pop_front().unwrap();
            for (offset_m, offset_n) in MOVE {
                if (item.0 == 0 && offset_m < 0) || (item.0 == m-1 && offset_m > 0) || (item.1 == 0 && offset_n < 0) || (item.1 == n-1 && offset_n > 0) {
                    continue;
                }

                let m_next: usize = (item.0 as i32 + offset_m) as usize;
                let n_next: usize = (item.1 as i32 + offset_n) as usize;
                if result[m_next][n_next] != i32::MAX {
                    continue;
                }

                match grid[m_next][n_next] {
                    1 => {
                        result[m_next][n_next] = item.2 + 1;
                        queue.push_back((m_next, n_next, result[m_next][n_next]));
                    },
                    0 | _ => {
                        result[m_next][n_next] = item.2;
                        queue.push_front((m_next, n_next, result[m_next][n_next]));
                    },
                };

            }
        }

        return result[m-1][n-1]
    }
}
```
