![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2981. [Find Longest Special Substring That Occurs Thrice I](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: the length of `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_length(s: String) -> i32 {
        let n: usize = s.len();
        let mut counter: HashMap<&str, i32> = HashMap::new();
        for index in 0..n {
            for index_end in index..n {
                if s[index..=index] != s[index_end..=index_end] {
                    break;
                }

                counter.entry(&s[index..=index_end]).and_modify(|value| *value += 1).or_insert(1);
            }
        }

        let mut result: i32 = -1;
        for (k, &v) in counter.iter() {
            if v < 3 {
                continue;
            }

            result = i32::max(result, k.len() as i32);
        }

        return result
    }
}
```

Method 2 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: the length of `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn maximum_length(s: String) -> i32 {
        let n: usize = s.len();
        let mut counter: HashMap<(&str, usize), i32> = HashMap::new();
        for index in 0..n {
            for index_end in index..n {
                if s[index..=index] != s[index_end..=index_end] {
                    break;
                }

                counter.entry((&s[index..=index_end], index_end-index+1)).and_modify(|value| *value += 1).or_insert(1);
            }
        }

        let mut result: i32 = -1;
        for (k, &v) in counter.iter() {
            if v < 3 {
                continue;
            }

            result = i32::max(result, k.1 as i32);
        }

        return result
    }
}
```
