![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 407. [Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*N*Log(M*N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `height_map`, N: the number of the elements in `height_map[0]`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    pub fn trap_rain_water(height_map: Vec<Vec<i32>>) -> i32 {
        let m: usize = height_map.len();
        let n: usize = height_map[0].len();
        let mut visited: Vec<Vec<bool>> = vec![vec![false; n]; m];
        let mut heap: BinaryHeap<(Reverse<i32>, usize, usize)> = BinaryHeap::new();
        for index_m in 0..m {
            heap.push((Reverse(height_map[index_m][0]), index_m, 0));
            heap.push((Reverse(height_map[index_m][n-1]), index_m, n-1));
            visited[index_m][0] = true;
            visited[index_m][n-1] = true;
        }
        for index_n in 0..n {
            heap.push((Reverse(height_map[0][index_n]), 0, index_n));
            heap.push((Reverse(height_map[m-1][index_n]), m-1, index_n));
            visited[0][index_n] = true;
            visited[m-1][index_n] = true;
        }

        let mut result: i32 = 0;
        while heap.len() > 0 {
            let (Reverse(height), index_m, index_n) = heap.pop().unwrap();

            for (offset_m, offset_n) in [(0, -1), (0, 1), (1, 0), (-1, 0)] {
                let index_m_next: usize = (index_m as i32 + offset_m) as usize;
                let index_n_next: usize = (index_n as i32 + offset_n) as usize;
                if index_m_next >= m || index_n_next >= n || visited[index_m_next][index_n_next] {
                    continue;
                }

                if height_map[index_m_next][index_n_next] < height {
                    result += height - height_map[index_m_next][index_n_next];
                }

                heap.push((Reverse(i32::max(height, height_map[index_m_next][index_n_next])), index_m_next, index_n_next));
                visited[index_m_next][index_n_next] = true;
            }
        }

        return result
    }
}
```
