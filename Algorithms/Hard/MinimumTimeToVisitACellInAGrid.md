![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2577. [Minimum Time To Visit A Cell In A Grid](https://leetcode.com/problems/minimum-time-to-visit-a-cell-in-a-grid)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 25/41) :
```rust
use std::collections::VecDeque;

const MOVE: [(i32, i32); 4] = [
    (0, -1),
    (0, 1),
    (-1, 0),
    (1, 0),
];
impl Solution {
    pub fn minimum_time(grid: Vec<Vec<i32>>) -> i32 {
        if grid[0][1] > 1 && grid[1][0] > 1 {
            return -1
        }

        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut counter: Vec<Vec<i32>> = vec![vec![i32::MAX; n]; m];
        let mut queue: VecDeque<(usize, usize, i32)> = VecDeque::from([(0, 0, 0)]);
        while queue.len() > 0 {
            let current: (usize, usize, i32) = queue.pop_front().unwrap();
            if current.2 >= counter[current.0][current.1] {
                continue;
            }
            counter[current.0][current.1] = current.2;

            for (offset_m, offset_n) in MOVE {
                if (offset_m < 0 && current.0 == 0) || (offset_m > 0 && current.0 == m-1) || (offset_n < 0 && current.1 == 0) || (offset_n > 0 && current.1 == n-1) {
                    continue;
                }

                let m_next: usize = (current.0 as i32 + offset_m) as usize;
                let n_next: usize = (current.1 as i32 + offset_n) as usize;
                if current.2 < grid[m_next][n_next]-1 {
                    match (grid[m_next][n_next]-current.2) % 2 {
                        0 => queue.push_back((m_next, n_next, grid[m_next][n_next]+1)),
                        1 | _ => queue.push_back((m_next, n_next, grid[m_next][n_next])),
                    };
                } else {
                    queue.push_back((m_next, n_next, current.2+1));
                }
            }
        }

        return counter[m-1][n-1]
    }
}
```

Method 2 (Dijkstra, Time Complexity: $O(M*N*Log(M*N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `grid`, N: the number of the elements in `grid[0]`)) :
```rust
use std::collections::{BinaryHeap, HashSet};
use std::cmp::Reverse;

const MOVE: [(i32, i32); 4] = [
    (0, -1),
    (0, 1),
    (-1, 0),
    (1, 0),
];
impl Solution {
    pub fn minimum_time(grid: Vec<Vec<i32>>) -> i32 {
        if grid[0][1] > 1 && grid[1][0] > 1 {
            return -1
        }

        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut heap: BinaryHeap<(Reverse<i32>, usize, usize)> = BinaryHeap::from([(Reverse(0), 0, 0)]);
        let mut visited: HashSet<(usize, usize)> = HashSet::new();
        while heap.len() > 0 {
            let current: (Reverse<i32>, usize, usize) = heap.pop().unwrap();
            let (Reverse(current_time), m_current, n_current) = current;
            if m_current == m-1 && n_current == n-1 {
                return current_time
            }

            if visited.contains(&(m_current, n_current)) {
                continue;
            }
            visited.insert((m_current, n_current));

            for (offset_m, offset_n) in MOVE {
                if (offset_m < 0 && m_current == 0) || (offset_m > 0 && m_current == m-1) || (offset_n < 0 && n_current == 0) || (offset_n > 0 && n_current == n-1) {
                    continue;
                }

                let m_next: usize = (m_current as i32 + offset_m) as usize;
                let n_next: usize = (n_current as i32 + offset_n) as usize;
                if current_time < grid[m_next][n_next]-1 {
                    match (grid[m_next][n_next]-current_time) % 2 {
                        0 => heap.push((Reverse(grid[m_next][n_next]+1), m_next, n_next)),
                        1 | _ => heap.push((Reverse(grid[m_next][n_next]), m_next, n_next)),
                    };
                } else {
                    heap.push((Reverse(current_time+1), m_next, n_next));
                }
            }
        }

        return -1
    }
}
```
