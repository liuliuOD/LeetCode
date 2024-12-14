![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2762. [Continuous Subarrays](https://leetcode.com/problems/continuous-subarrays)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn continuous_subarrays(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut mapping: HashMap<i32, usize> = HashMap::new();
        let mut result: i64 = 0;
        for right in 0..n {
            let num: i32 = nums[right];
            for (k, v) in mapping.clone() {
                if (k-num).abs() <= 2 {
                    continue;
                }

                left = usize::max(left, v+1);
                mapping.remove(&k);
            }
            mapping.insert(num, right);

            result += (right-left+1) as i64;
        }

        return result
    }
}
```
