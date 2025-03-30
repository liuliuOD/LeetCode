![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 763. [Partition Labels](https://leetcode.com/problems/partition-labels)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `s`)) :
```rust
impl Solution {
    const BASE: u8 = b'a';

    pub fn partition_labels(s: String) -> Vec<i32> {
        let s_bytes: &[u8] = s.as_bytes();
        let n: usize = s_bytes.len();
        let mut mapping: [usize; 26] = [0; 26];
        for index in 0..n {
            mapping[(s_bytes[index]-Self::BASE) as usize] = index;
        }

        let mut result: Vec<i32> = Vec::new();
        let mut amount_cumulative: i32 = 0;
        let mut maximum: i32 = -1;
        for index in 0..n {
            let ascii: u8 = s_bytes[index];
            let index_ascii_last: usize = (ascii-Self::BASE) as usize;
            if maximum < mapping[index_ascii_last] as i32 {
                maximum = mapping[index_ascii_last] as i32;
            }
            if index == maximum as usize {
                result.push(index as i32 + 1 - amount_cumulative);
                amount_cumulative = index as i32 + 1;
                maximum = -1;
            }
        }

        return result
    }
}
```
