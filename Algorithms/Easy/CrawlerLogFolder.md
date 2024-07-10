![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1598. [Crawler Log Folder](https://leetcode.com/problems/crawler-log-folder)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```Rust
impl Solution {
    pub fn min_operations(logs: Vec<String>) -> i32 {
        let mut current: i32 = 0;
        for log in logs {
            match log.as_str() {
                "../" if current > 0 => current -= 1,
                "./" | "../" => {},
                _ => current += 1,
            };
        }

        return current
    }
}
```
