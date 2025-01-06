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

Method 2 (Brute Force + Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `boxes`)) :
```rust
impl Solution {
    pub fn min_operations(boxes: String) -> Vec<i32> {
        let n: usize = boxes.len();
        let mut result: Vec<i32> = vec![0; n];
        for (index, ascii) in boxes.bytes().enumerate() {
            if ascii == b'0' {
                continue;
            }

            for index_neighbor in 0..n {
                result[index_neighbor] += (index as i32 - index_neighbor as i32).abs();
            }
        }

        return result
    }
}
```

Method 3 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `boxes`)) :
```rust
impl Solution {
    pub fn min_operations(boxes: String) -> Vec<i32> {
        let n: usize = boxes.len();
        let boxes_byte: Vec<u8> = boxes.into_bytes();
        let mut result: Vec<i32> = vec![0; n];

        let mut amount: i32 = 0;
        for index in 0..n {
            let ascii: u8 = boxes_byte[index];

            result[index] = amount;
            if index > 0 {
                result[index] += result[index-1];
            }

            if ascii == b'1' {
                amount += 1;
            }
        }

        amount = 0;
        let mut cumulative: i32 = 0;
        for index in (0..n).rev() {
            let ascii: u8 = boxes_byte[index];

            result[index] += cumulative;

            if ascii == b'1' {
                amount += 1;
            }
            cumulative += amount;
        }

        return result
    }
}
```
