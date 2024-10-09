![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 921. [Minimum Add To Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_add_to_make_valid(s: String) -> i32 {
        let mut left: i32 = 0;
        let mut right: i32 = 0;
        for character in s.chars() {
            if character == '(' {
                left += 1;
            } else if left > 0 {
                left -= 1;
            } else {
                right += 1;
            }
        }

        return left + right
    }
}
```
