![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 664. [Strange Printer](https://leetcode.com/problems/strange-printer)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N^3)$, Space Complexity: $O(N^2)$ (N: the number of the elements in `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn strange_printer(s: String) -> i32 {
        let mut s_vec: Vec<u8> = s.into_bytes();
        s_vec.dedup();
        let mut memoization: HashMap<(usize, usize), i32> = HashMap::new();

        return Self::dfs(0, s_vec.len()-1, &s_vec, &mut memoization)
    }

    fn dfs(index_start: usize, index_end: usize, s_vec: &Vec<u8>, memoization: &mut HashMap<(usize, usize), i32>) -> i32 {
        if index_start > index_end {
            return 0
        }

        let key: (usize, usize) = (index_start, index_end);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: i32 = 1 + Self::dfs(index_start+1, index_end, s_vec, memoization);
        for index_current in index_start+1..=index_end {
            if s_vec[index_current] != s_vec[index_start] {
                continue;
            }

            result = i32::min(result, Self::dfs(index_start, index_current-1, s_vec, memoization)+Self::dfs(index_current+1, index_end, s_vec, memoization));
        }
        memoization.insert(key, result);
        return *memoization.get(&key).unwrap()
    }
}
```
