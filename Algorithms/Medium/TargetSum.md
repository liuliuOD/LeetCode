![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 494. [Target Sum](https://leetcode.com/problems/target-sum)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N^2)$, Space Complexity: $O(N^)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_target_sum_ways(nums: Vec<i32>, target: i32) -> i32 {
        let mut counter: HashMap<i32, i32> = HashMap::from([(0, 1)]);
        for &num in nums.iter() {
            let mut temp: HashMap<i32, i32> = HashMap::new();
            for (key, amount) in counter {
                temp.entry(key+num).and_modify(|item| *item += amount).or_insert(amount);
                temp.entry(key-num).and_modify(|item| *item += amount).or_insert(amount);
            }
            counter = temp;
        }

        return match counter.get(&target) {
            Some(result) => *result,
            None => 0,
        }
    }
}
```
