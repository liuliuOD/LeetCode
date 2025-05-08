![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3342. [Find Minimum Time To Reach Last Room II](https://leetcode.com/problems/find-minimum-time-to-reach-last-room-ii)

### Solution :

Method 1 (Dijkstra, Time Complexity: $O(M*N*Log(M*N))$, Space Complexity: $O(M*N)$ (N: the number of elements in `move_time`, M: the number of elements in `move_time[0]`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    const DIR: [(i32, i32); 4] = [(0, 1), (0, -1), (1, 0), (-1, 0)];

    pub fn min_time_to_reach(move_time: Vec<Vec<i32>>) -> i32 {
        let n: usize = move_time.len();
        let m: usize = move_time[0].len();
        let mut visited: Vec<Vec<bool>> = vec![vec![false; m]; n];
        let mut distances: Vec<Vec<i32>> = vec![vec![i32::MAX; m]; n];
        distances[0][0] = 0;
        let mut heap: BinaryHeap<(Reverse<i32>, Reverse<i32>, usize, usize)> = BinaryHeap::from([(Reverse(0), Reverse(1), 0, 0)]);
        while heap.len() > 0 {
            let (Reverse(distance), Reverse(cost), i, j) = heap.pop().unwrap();
            if visited[i][j] {
                continue;
            }
            visited[i][j] = true;

            for (offset_i, offset_j) in Self::DIR {
                let i_next: usize = (i as i32 + offset_i) as usize;
                let j_next: usize = (j as i32 + offset_j) as usize;
                if i_next >= n || j_next >= m {
                    continue;
                }

                let distance_current: i32 = cost + i32::max(distances[i][j], move_time[i_next][j_next]);
                if distance_current < distances[i_next][j_next] {
                    distances[i_next][j_next] = distance_current;
                    let cost_next: i32 = match cost {
                        2 => 1,
                        _ => 2,
                    };
                    heap.push((Reverse(distance_current), Reverse(cost_next), i_next, j_next));
                }
            }
        }

        return distances[n-1][m-1]
    }
}
```
