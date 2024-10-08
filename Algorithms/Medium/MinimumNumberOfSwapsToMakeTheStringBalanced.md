![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1963. [Minimum Number Of Swaps To Make The String Balanced](https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_swaps(s: String) -> i32 {
        let mut left: i32 = 0;
        let mut right: i32 = 0;
        for ascii in s.bytes() {
            if ascii == b'[' {
                left += 1;
            } else if left > 0 {
                left -= 1;
            } else {
                right += 1;
            }
        }

        return ((left + right)/2 + 1) / 2
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_swaps(s: String) -> i32 {
        let mut left: i32 = 0;
        for ascii in s.bytes() {
            if ascii == b'[' {
                left += 1;
            } else if left > 0 {
                left -= 1;
            }
        }

        return (left + 1) / 2
    }
}
```
