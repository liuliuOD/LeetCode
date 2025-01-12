![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2116. [Check If A Parentheses String Can Be Valid](https://leetcode.com/problems/check-if-a-parentheses-string-can-be-valid)

### Solution :

Method 1 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn can_be_valid(s: String, locked: String) -> bool {
        let n: usize = s.len();
        if n % 2 == 1 {
            return false
        }

        let s_bytes: Vec<u8> = s.into_bytes();
        let locked_bytes: Vec<u8> = locked.into_bytes();
        let mut open: Vec<usize> = Vec::new();
        let mut unlocked: Vec<usize> = Vec::new();
        for index in 0..n {
            if locked_bytes[index] == b'0' {
                unlocked.push(index);
                continue;
            }

            match s_bytes[index] {
                b'(' => {
                    open.push(index);
                },
                b')' | _ => {
                    if open.len() > 0 {
                        open.pop();
                    } else if unlocked.len() > 0 {
                        unlocked.pop();
                    } else {
                        return false
                    }
                }
            }
        }

        while open.len() > 0 && unlocked.len() > 0 && *open.last().unwrap() < *unlocked.last().unwrap() {
            open.pop();
            unlocked.pop();
        }

        return open.len() == 0
    }
}
```
