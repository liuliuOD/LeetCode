![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1769. [Minimum Number Of Operations To Move All Balls To Each Box](https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `boxes`)) :
```rust
impl Solution {
    pub fn min_operations(boxes: String) -> Vec<i32> {
        let n: usize = boxes.len();
        let mut mapping: Vec<bool> = vec![false; n];
        for (index, ascii) in boxes.bytes().enumerate() {
            if ascii == b'1' {
                mapping[index] = true;
            }
        }

        let mut result: Vec<i32> = vec![0; n];
        for index in 0..n {
            for index_neighbor in 0..n {
                if mapping[index_neighbor] {
                    result[index] += (index as i32 - index_neighbor as i32).abs();
                }
            }
        }

        return result
    }
}
```
