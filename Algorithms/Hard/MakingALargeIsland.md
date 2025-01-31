![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 827. [Making A Large Island](https://leetcode.com/problems/making-a-large-island)

### Solution :

Method 1 (BFS, Time Complexity: $O(M*N)$, Space Complexity: $O(MAX(M, N))$ (M: the number of the elements in `grid`, N: the number of the elements in `grid[0]`)) :
```rust
use std::collections::{HashMap, VecDeque};

impl Solution {
    pub fn largest_island(mut grid: Vec<Vec<i32>>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut counter: HashMap<usize, i32> = HashMap::new();
        let mut index_counter: usize = 2;
        for index_m in 0..m {
            for index_n in 0..n {
                Self::bfs(index_m, index_n, &mut index_counter, &mut counter, &mut grid);
            }
        }

        let mut result: i32 = i32::MIN;
        for index_m in 0..m {
            for index_n in 0..n {
                if grid[index_m][index_n] != 0 {
                    continue;
                }

                result = i32::max(result, Self::calculate_island_size(index_m, index_n, &grid, &counter));
            }
        }

        return match result {
            i32::MIN => (m*n) as i32,
            _ => result,
        }
    }

    fn bfs(index_m: usize, index_n: usize, index_counter: &mut usize, counter: &mut HashMap<usize, i32>, grid: &mut Vec<Vec<i32>>) {
        if grid[index_m][index_n] == 0 {
            return
        }

        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut queue: VecDeque<(usize, usize)> = VecDeque::from([(index_m, index_n)]);
        while queue.len() > 0 {
            let (index_m_current, index_n_current) = queue.pop_front().unwrap();
            if grid[index_m_current][index_n_current] != 1 {
                continue;
            }
            grid[index_m_current][index_n_current] = *index_counter as i32;
            counter.entry(*index_counter).and_modify(|value| *value += 1).or_insert(1);

            for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                let index_m_next: usize = (index_m_current as i32 + offset_m) as usize;
                let index_n_next: usize = (index_n_current as i32 + offset_n) as usize;
                if index_m_next >= m || index_n_next >= n || grid[index_m_next][index_n_next] != 1 {
                    continue;
                }

                queue.push_back((index_m_next, index_n_next));
            }
        }

        *index_counter += 1;
    }

    fn calculate_island_size(index_m: usize, index_n: usize, grid: &Vec<Vec<i32>>, counter: &HashMap<usize, i32>) -> i32 {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut result: i32 = 1;
        let mut visited: Vec<usize> = Vec::new();
        for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
            let index_m_next: usize = (index_m as i32 + offset_m) as usize;
            let index_n_next: usize = (index_n as i32 + offset_n) as usize;
            if index_m_next >= m || index_n_next >= n || grid[index_m_next][index_n_next] == 0 {
                continue;
            }

            let index_counter: usize = grid[index_m_next][index_n_next] as usize;
            if visited.contains(&index_counter) {
                continue;
            }
            visited.push(index_counter);
            result += *counter.get(&index_counter).unwrap();
        }

        return result
    }
}
```
