![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2094. [Finding 3-Digit Even Numbers](https://leetcode.com/problems/finding-3-digit-even-numbers)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N^3)$, Space Complexity: $O(N)$ (N: the number of the elements in `digits`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_even_numbers(digits: Vec<i32>) -> Vec<i32> {
        let n: usize = digits.len();
        let mut result: HashSet<i32> = HashSet::new();
        for index_first in 0..n {
            if digits[index_first] == 0 {
                continue;
            }

            for index_second in 0..n {
                if index_second == index_first {
                    continue;
                }

                for index_last in 0..n {
                    if index_last == index_second ||
                        index_last == index_first ||
                        digits[index_last]%2 == 1 {
                        continue;
                    }

                    result.insert(digits[index_first]*100 + digits[index_second]*10 + digits[index_last]);
                }
            }
        }

        let mut result: Vec<i32> = result.into_iter().collect::<Vec<i32>>();
        result.sort();
        return result
    }
}
```
