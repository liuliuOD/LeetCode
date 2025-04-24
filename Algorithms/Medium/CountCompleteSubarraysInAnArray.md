![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2799. [Count Complete Subarrays In An Array](https://leetcode.com/problems/count-complete-subarrays-in-an-array)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::{HashMap, HashSet};

impl Solution {
    pub fn count_complete_subarrays(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let unique_nums: HashSet<i32> = HashSet::from_iter(nums.iter().map(|num| *num));
        let amount_unique: usize = unique_nums.len();
        let mut counter: HashMap<i32, i32> = HashMap::new();
        let mut left: usize = 0;
        let mut right: usize = 0;
        let mut result: i32 = 0;
        while right < n {
            counter.entry(nums[right]).and_modify(|amount| *amount += 1).or_insert(1);

            while counter.len() == amount_unique {
                result += (n-right) as i32;

                counter.entry(nums[left]).and_modify(|amount| *amount -= 1);
                if *counter.get(&nums[left]).unwrap() == 0 {
                    counter.remove(&nums[left]);
                }

                left += 1;
            }

            right += 1;
        }

        return result
    }
}
```
