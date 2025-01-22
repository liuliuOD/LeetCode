![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1765. [Map Of Highest Peak](https://leetcode.com/problems/map-of-highest-peak)

### Solution :

Method 1 (Queue, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `is_water`, N: the number of the elements in `is_water[0]`)) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn highest_peak(is_water: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m: usize = is_water.len();
        let n: usize = is_water[0].len();
        let mut queue: VecDeque<(i32, usize, usize)> = VecDeque::new();
        for index_m in 0..m {
            for index_n in 0..n {
                if is_water[index_m][index_n] == 1 {
                    queue.push_back((0, index_m, index_n));
                }
            }
        }

        let mut result: Vec<Vec<i32>> = vec![vec![0; n]; m];
        let mut visited: Vec<Vec<bool>> = vec![vec![false; n]; m];
        while queue.len() > 0 {
            let (height, index_m, index_n) = queue.pop_front().unwrap();
            if visited[index_m][index_n] {
                continue;
            }
            visited[index_m][index_n] = true;
            result[index_m][index_n] = height;

            for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                let index_m_next: usize = (index_m as i32 + offset_m) as usize;
                let index_n_next: usize = (index_n as i32 + offset_n) as usize;
                if index_m_next >= m || index_n_next >= n {
                    continue;
                }

                queue.push_back((height+1, index_m_next, index_n_next));
            }
        }

        return result
    }
}
```

Method 2 (Queue, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the number of the elements in `is_water`, N: the number of the elements in `is_water[0]`)) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn highest_peak(is_water: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m: usize = is_water.len();
        let n: usize = is_water[0].len();
        let mut queue: VecDeque<(usize, usize)> = VecDeque::new();
        for index_m in 0..m {
            for index_n in 0..n {
                if is_water[index_m][index_n] == 1 {
                    queue.push_back((index_m, index_n));
                }
            }
        }

        let mut result: Vec<Vec<i32>> = vec![vec![0; n]; m];
        let mut height: i32 = 0;
        let mut visited: Vec<Vec<bool>> = vec![vec![false; n]; m];
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let (index_m, index_n) = queue.pop_front().unwrap();
                if visited[index_m][index_n] {
                    continue;
                }
                visited[index_m][index_n] = true;
                result[index_m][index_n] = height;

                for (offset_m, offset_n) in [(0, 1), (0, -1), (1, 0), (-1, 0)] {
                    let index_m_next: usize = (index_m as i32 + offset_m) as usize;
                    let index_n_next: usize = (index_n as i32 + offset_n) as usize;
                    if index_m_next >= m || index_n_next >= n {
                        continue;
                    }

                    queue.push_back((index_m_next, index_n_next));
                }
            }

            height += 1;
        }

        return result
    }
}
```
