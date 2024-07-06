![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2582. [Pass The Pillow](https://leetcode.com/problems/pass-the-pillow)

### Solution :

Method 1 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```Rust
impl Solution {
    pub fn pass_the_pillow(n: i32, time: i32) -> i32 {
        return match time/(n - 1) % 2 {
            0 => time%(n - 1) + 1,
            1 | _ => n - (time%(n - 1))
        }
    }
}
```
