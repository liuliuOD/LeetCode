![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2326. [Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv)

### Solution :

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
//
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
```

Method 1 (Simulation, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: value of `m`, N: value of `n`)) :
```rust
const DIRECTIONS: [(i32, i32); 4] = [(0, 1), (1, 0), (0, -1), (-1, 0)];
type Custom = Box<ListNode>;

impl Solution {
    pub fn spiral_matrix(m: i32, n: i32, mut head: Option<Custom>) -> Vec<Vec<i32>> {
        let m: usize = m as usize;
        let n: usize = n as usize;
        let mut result: Vec<Vec<i32>> = vec![vec![-1; n]; m];
        if head.is_none() {
            return result
        }

        let mut index_m: usize = 0;
        let mut index_n: usize = 0;
        let mut index_direction: usize = 0;
        let mut current: &mut Option<Custom> = &mut head;
        while let Some(inner) = current {
            while result[index_m][index_n] != -1 {
                let mut index_m_next: usize = (index_m as i32 + DIRECTIONS[index_direction].0) as usize;
                let mut index_n_next: usize = (index_n as i32 + DIRECTIONS[index_direction].1) as usize;
                if index_m_next >= m || index_n_next >= n || result[index_m_next][index_n_next] != -1 {
                    index_direction = (index_direction+1) % 4;
                } else {
                    index_m = index_m_next;
                    index_n = index_n_next;
                }
            }

            result[index_m][index_n] = inner.val;
            current = &mut inner.next;
        }

        return result
    }
}
```
