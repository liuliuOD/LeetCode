![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1593. [Split A String Into The Max Number Of Unique Substrings](https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(N*2^N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn max_unique_split(s: String) -> i32 {
        let mut visited: HashSet<&str> = HashSet::new();
        return Self::backtracking(0, &s, &mut visited)
    }

    fn backtracking<'a>(index: usize, s: &'a str, mut visited: &mut HashSet<&'a str>) -> i32 {
        if index >= s.len() {
            return visited.len() as i32
        }

        let mut result: i32 = 0;
        for index_end in index..s.len() {
            if visited.contains(&s[index..=index_end]) {
                continue;
            }

            visited.insert(&s[index..=index_end]);
            result = i32::max(result, Self::backtracking(index_end+1, s, visited));
            visited.remove(&s[index..=index_end]);
        }

        return result
    }
}
```
