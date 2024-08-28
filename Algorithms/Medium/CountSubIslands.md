![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1905. [Count Sub Islands](https://leetcode.com/problems/count-sub-islands)

### Solution :

Method 1 (BFS, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `grid1`, N: the number of the elements in `grid1[0]`)) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn count_sub_islands(mut grid1: Vec<Vec<i32>>, mut grid2: Vec<Vec<i32>>) -> i32 {
        let m: usize = grid1.len();
        let n: usize = grid1[0].len();
        let mut color_current: i32 = 2;
        for index_m in 0..m {
            for index_n in 0..n {
                Self::bfs(index_m, index_n, color_current, &mut grid1);
                color_current += 1;
            }
        }

        let mut result: i32 = 0;
        for index_m in 0..m {
            for index_n in 0..n {
                result += Self::bfs_sub_islands(index_m, index_n, &grid1, &mut grid2);
            }
        }

        return result
    }

    fn bfs(index_m: usize, index_n: usize, color: i32, grid: &mut Vec<Vec<i32>>) {
        let mut queue: VecDeque<(usize, usize)> = VecDeque::from([(index_m, index_n)]);
        while !queue.is_empty() {
            let point: (usize, usize) = queue.pop_front().unwrap();
            if grid[point.0][point.1] != 1 {
                continue;
            }
            grid[point.0][point.1] = color;

            for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                let mut index_m_next: usize = point.0;
                if offset_m >= 0 {
                    index_m_next += offset_m as usize;
                } else {
                    index_m_next -= (offset_m as i32).abs() as usize;
                }
                let mut index_n_next: usize = point.1;
                if offset_n >= 0 {
                    index_n_next += offset_n as usize;
                } else {
                    index_n_next -= (offset_n as i32).abs() as usize;
                }

                if index_m_next >= grid.len() || index_n_next >= grid[0].len() || grid[index_m_next][index_n_next] != 1 {
                    continue;
                }
                queue.push_back((index_m_next, index_n_next));
            }
        }
    }

    fn bfs_sub_islands(index_m: usize, index_n: usize, grid1: &Vec<Vec<i32>>, grid2: &mut Vec<Vec<i32>>) -> i32 {
        let mut queue: VecDeque<(usize, usize)> = VecDeque::from([(index_m, index_n)]);
        let island_current: i32 = grid1[index_m][index_n];
        let mut result: bool = grid2[index_m][index_n] == 1 && grid1[index_m][index_n] > 0;
        while !queue.is_empty() {
            let point: (usize, usize) = queue.pop_front().unwrap();
            if grid2[point.0][point.1] != 1 {
                continue;
            }
            grid2[point.0][point.1] = 2;
            if grid1[point.0][point.1] != island_current {
                result = false;
            }

            for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                let mut index_m_next: usize = point.0;
                if offset_m >= 0 {
                    index_m_next += offset_m as usize;
                } else {
                    index_m_next -= (offset_m as i32).abs() as usize;
                }
                let mut index_n_next: usize = point.1;
                if offset_n >= 0 {
                    index_n_next += offset_n as usize;
                } else {
                    index_n_next -= (offset_n as i32).abs() as usize;
                }

                if index_m_next >= grid2.len() || index_n_next >= grid2[0].len() || grid2[index_m_next][index_n_next] != 1 {
                    continue;
                }
                queue.push_back((index_m_next, index_n_next));
            }
        }

        return match result {
            true => 1,
            false => 0,
        }
    }
}
```
