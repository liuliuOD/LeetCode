![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2845. [Count Of Interesting Subarrays](https://leetcode.com/problems/count-of-interesting-subarrays)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(MIN(M, N))$ (M: the value of `modulo`, N: the number of the elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn count_interesting_subarrays(nums: Vec<i32>, modulo: i32, k: i32) -> i64 {
        let n: usize = nums.len();
        let mut remainder: i32 = 0;
        let mut result: i64 = 0;
        let mut mapping: HashMap<i32, i64> = HashMap::new();
        for (index, num) in nums.into_iter().enumerate() {
            if num%modulo == k {
                remainder = (remainder+1) % modulo;
            }

            if remainder == k {
                result += 1;
            }
            let key: i32 = match k == 0 {
                true => remainder,
                _ => (remainder+modulo-k) % modulo,
            };
            if mapping.get(&key).is_some() {
                result += *mapping.get(&key).unwrap();
            }

            mapping.entry(remainder).and_modify(|amount| *amount += 1).or_insert(1);
        }

        return result
    }
}
```
