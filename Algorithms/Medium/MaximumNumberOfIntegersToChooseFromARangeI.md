![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2554. [Maximum Number Of Integers To Choose From A Range I](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-i)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `banned`, N: the value of `n`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn max_count(banned: Vec<i32>, n: i32, max_sum: i32) -> i32 {
        let mut set: HashSet<i32> = HashSet::from_iter(banned);
        let mut sum: i64 = 0;
        let mut result: i32 = 0;
        for num in 1..=n {
            if set.contains(&num) {
                continue;
            }

            sum += num as i64;
            result += 1;
            /* Option 1 */
            if sum > max_sum as i64 {
                result -= 1;
                break;
            } else if sum == max_sum as i64 {
                break;
            }
            /* Option 2

            if sum < max_sum as i64 {
                continue;
            }

            if sum > max_sum as i64 {
                result -= 1;
            }
            break;
            */
        }

        return result
    }
}
```
