![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1408. [String Matching In An Array](https://leetcode.com/problems/string-matching-in-an-array)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `words`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn string_matching(mut words: Vec<String>) -> Vec<String> {
        let n: usize = words.len();
        words.sort_by_key(|item| item.len());
        let mut substrings: HashSet<String> = HashSet::new();
        for index in 0..n {
            for index_another in index+1..n {
                if words[index_another].contains(&words[index]) {
                    substrings.insert(words[index].clone());
                    break;
                }
            }
        }

        return Vec::from_iter(substrings)
    }
}
```
