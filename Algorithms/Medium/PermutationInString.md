![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 567. [Permutation In String](https://leetcode.com/problems/permutation-in-string)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (N: the length of `s1`, M: the length of `s2`)) :
```rust
const BASE: usize = 'a' as usize;
impl Solution {
    pub fn check_inclusion(s1: String, s2: String) -> bool {
        let mut counter: [i32; 26] = [0; 26];
        for character in s1.chars() {
            counter[character as usize - BASE] += 1;
        }

        let n: usize = s1.len();
        let mut counter_s2: [i32; 26] = [0; 26];
        let s2_bytes: Vec<u8> = s2.into_bytes();
        for (index, &character) in s2_bytes.iter().enumerate() {
            counter_s2[character as usize - BASE] += 1;

            if index >= n {
                counter_s2[s2_bytes[index-n] as usize - BASE] -= 1;
            }

            let mut is_contain: bool = true;
            for (index, &amount) in counter.iter().enumerate() {
                if amount != counter_s2[index] {
                    is_contain = false;
                    break;
                }
            }

            if is_contain {
                return true
            }
        }

        return false
    }
}
```
