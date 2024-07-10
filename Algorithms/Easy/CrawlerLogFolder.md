![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1598. [Crawler Log Folder](https://leetcode.com/problems/crawler-log-folder)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `logs`)) :
```Rust
impl Solution {
    pub fn min_operations(logs: Vec<String>) -> i32 {
        let mut current: i32 = 0;
        for log in logs {
            match log.as_str() {
                /* Option 1 */
                "../" if current > 0 => current -= 1,
                "../" | "./" => {},
                /* Option 2

                "./" => {},
                "../" => current = 0.max(current-1),
                */
                _ => current += 1,
            };
        }

        return current
    }
}
```

Method 2 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `logs`)) :
```rust
impl Solution {
    pub fn min_operations(logs: Vec<String>) -> i32 {
        let mut stack: Vec<String> = vec![];
        for log in logs {
            match log.as_str() {
                "../" if stack.len() > 0 => {
                    stack.pop();
                },
                "../" | "./" => {},
                path => stack.push(path.to_string()),
            };
        }

        return stack.len() as i32
    }
}
```
