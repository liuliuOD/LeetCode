![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1684. [Count The Number Of Consistent Strings](https://leetcode.com/problems/count-the-number-of-consistent-strings)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M*N)$, Space Complexity: $O(P)$ (M: the number of the elements in `words`, N: the average length of each element in `words`, P: the length of `allowed`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn count_consistent_strings(allowed: String, words: Vec<String>) -> i32 {
        let allowed_set: HashSet<u8> = HashSet::from_iter(allowed.into_bytes());
        let mut result: i32 = 0;
        for word in words {
            let mut is_consistent: bool = true;
            for character in word.as_bytes() {
                if !allowed_set.contains(&character) {
                    is_consistent = false;
                    break;
                }
            }

            if is_consistent {
                result += 1;
            }
        }

        return result
    }
}
```
