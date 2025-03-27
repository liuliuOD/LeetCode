![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2780. [Minimum Index Of A Valid Split](https://leetcode.com/problems/minimum-index-of-a-valid-split)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn minimum_index(nums: Vec<i32>) -> i32 {
        let mut counter: HashMap<i32, usize> = HashMap::new();
        let mut maximum_num: i32 = 0;
        let mut maximum_amount: usize = 0;
        for num in &nums {
            counter.entry(*num).and_modify(|amount| *amount += 1).or_insert(1);
            if *counter.get(num).unwrap() > maximum_amount {
                maximum_amount = *counter.get(num).unwrap();
                maximum_num = *num;
            }
        }

        let n: usize = nums.len();
        if n/2 >= maximum_amount {
            return -1
        }

        let mut current_maximum_amount: usize = 0;
        for index in 0..n-1 {
            if nums[index] == maximum_num {
                current_maximum_amount += 1;
            }

            if current_maximum_amount > (index+1)/2 && (maximum_amount-current_maximum_amount) > (n-index-1)/2 {
                return index as i32
            }
        }

        return -1
    }
}
```
