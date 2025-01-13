![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3223. [Minimum Length Of String After Operations](https://leetcode.com/problems/minimum-length-of-string-after-operations)

### Solution :

Method 1 (Counter, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn minimum_length(s: String) -> i32 {
        let mut counter: [i32; 26] = [0; 26];
        for ascii in s.bytes() {
            counter[(ascii-BASE) as usize] += 1;
        }

        return counter.iter().fold(0, |accumulate, amount| {
            if *amount == 0 {
                return accumulate
            }

            if *amount % 2 == 0 {
                return accumulate + 2
            }
            return accumulate + 1
        })
    }
}
```
