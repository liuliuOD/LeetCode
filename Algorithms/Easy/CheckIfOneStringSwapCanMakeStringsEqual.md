![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1790. [Check If One String Swap Can Make Strings Equal](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s1`)) :
```rust
impl Solution {
    pub fn are_almost_equal(s1: String, s2: String) -> bool {
        let s1_asciis: Vec<u8> = s1.into_bytes();
        let s2_asciis: Vec<u8> = s2.into_bytes();
        let mut s1_diff_ascii: u8 = 0;
        let mut s2_diff_ascii: u8 = 0;
        let mut is_swapped: bool = true;
        for index in 0..s1_asciis.len() {
            if s1_asciis[index] == s2_asciis[index] {
                continue;
            }

            if s1_diff_ascii == 0 {
                s1_diff_ascii = s1_asciis[index];
                s2_diff_ascii = s2_asciis[index];
                is_swapped = false;
                continue;
            }

            if s1_diff_ascii != s2_asciis[index] || s2_diff_ascii != s1_asciis[index] {
                return false
            }

            if is_swapped {
                return false
            }
            is_swapped = true;
        }

        return is_swapped
    }
}
```
