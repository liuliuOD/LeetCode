![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1358. [Number Of Substrings Containing All Three Characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn number_of_substrings(s: String) -> i32 {
        let n: i32 = s.len() as i32;
        let mut counter: [i32; 3] = [0; 3];
        let mut left: i32 = 0;
        let mut s_bytes: &[u8] = s.as_bytes();
        let mut result: i32 = 0;
        for right in 0..n {
            counter[(s_bytes[right as usize]-BASE) as usize] += 1;

            while left <= right && counter[0] > 0 && counter[1] > 0 && counter[2] > 0 {
                result += n - right;
                counter[(s_bytes[left as usize]-BASE) as usize] -= 1;
                left += 1;
            }
        }

        return result
    }
}
```
