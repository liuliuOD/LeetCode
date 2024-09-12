![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1684. [Count The Number Of Consistent Strings](https://leetcode.com/problems/count-the-number-of-consistent-strings)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M*N+P)$, Space Complexity: $O(P)$ (M: the number of the elements in `words`, N: the average length of each element in `words`, P: the length of `allowed`)) :
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

Method 2 (Bitmask, Time Complexity: $O(M*N+P)$, Space Complexity: $O(1)$ (M: the number of the elements in `words`, N: the average length of each element in `words`, P: the length of `allowed`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn count_consistent_strings(allowed: String, words: Vec<String>) -> i32 {
        let mut mask: i32 = 0;
        for ch in allowed.as_bytes() {
            mask |= 1 << (ch - BASE);
        }

        let mut result: i32 = 0;
        for word in words {
            /* Option 1 */
            let mut is_consistent: bool = true;
            for ch in word.as_bytes() {
                if mask & 1 << (ch - BASE) == 0 {
                    is_consistent = false;
                    break;
                }
            }

            if is_consistent {
                result += 1;
            }
            /* Option 2

            result += 1;
            for ch in word.as_bytes() {
                if mask & 1 << (ch - BASE) == 0 {
                    result -= 1;
                    break;
                }
            }
            */
        }

        return result
    }
}
```
