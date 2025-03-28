![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2503. [Maximum Number Of Points From Grid Queries](https://leetcode.com/problems/maximum-number-of-points-from-grid-queries)

### Solution :

Method 1 (Hash Set + BFS, Time Complexity: $O(J*K*N+N*Log(N))$, Space Complexity: $O(J*K)$ (J: the number of elements in `grid`, K: the number of elements in `grid[0]`, N: the number of elements in `queries`)) :
```rust
use std::collections::{VecDeque, HashSet};

impl Solution {
    pub fn max_points(grid: Vec<Vec<i32>>, queries: Vec<i32>) -> Vec<i32> {
        let j: usize = grid.len();
        let k: usize = grid[0].len();
        let n: usize = queries.len();
        let mut queries: Vec<(i32, usize)> = queries.iter().enumerate().map(|(index, num)| (*num, index)).collect();
        queries.sort_unstable();
        let mut result: Vec<i32> = vec![0; n];
        let mut visited: HashSet<(usize, usize)> = HashSet::new();
        let mut candidates: HashSet<(usize, usize)> = HashSet::from([(0, 0)]);
        let mut queue: VecDeque<(usize, usize)> = VecDeque::new();
        for (query, index) in queries {
            for candidate in candidates.iter().copied().collect::<Vec<(usize, usize)>>() {
                if grid[candidate.0][candidate.1] >= query {
                    continue;
                }

                queue.push_back((candidate.0, candidate.1));
                candidates.remove(&candidate);
            }

            while queue.len() > 0 {
                let (x, y) = queue.pop_front().unwrap();
                if visited.contains(&(x, y)) {
                    continue;
                }
                if grid[x][y] >= query {
                    candidates.insert((x, y));
                    continue;
                }
                visited.insert((x, y));

                for (offset_x, offset_y) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                    if (x == 0 && offset_x < 0) || (x == j-1 && offset_x > 0) || (y == 0 && offset_y < 0) || (y == k-1 && offset_y > 0) {
                        continue;
                    }

                    let x_next: usize = (x as i32 + offset_x) as usize;
                    let y_next: usize = (y as i32 + offset_y) as usize;
                    queue.push_back((x_next, y_next));
                }
            }

            result[index] = visited.len() as i32;
        }

        return result
    }
}
````
