![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3210. [Find The Encrypted String](https://leetcode.com/problems/find-the-encrypted-string)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```Rust
impl Solution {
    pub fn get_encrypted_string(s: String, k: i32) -> String {
        let n: usize = s.len();
        let mut result: String = String::new();
        for index in 0..n {
            let index_replace: usize = (index + k as usize) % n;
            result += &s[index_replace..index_replace+1];
        }

        return result
    }
}
```
