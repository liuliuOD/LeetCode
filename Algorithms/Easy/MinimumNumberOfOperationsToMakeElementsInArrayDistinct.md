![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3396. [Minimum Number Of Operations To Make Elements In Array Distinct](https://leetcode.com/problems/minimum-number-of-operations-to-make-elements-in-array-distinct)

### Solution :

Method 1 (Hash Map + Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::{HashMap, HashSet};

impl Solution {
    pub fn minimum_operations(nums: Vec<i32>) -> i32 {
        let mut counter: HashMap<i32, usize> = HashMap::new();
        let mut duplicate: HashSet<i32> = HashSet::new();
        for &num in &nums {
            counter.entry(num).and_modify(|amount| *amount += 1).or_insert(1);
            if *counter.get(&num).unwrap() == 2 {
                duplicate.insert(num);
            }
        }

        let n: usize = nums.len();
        let mut result: i32 = 0 ;
        let mut index: usize = 0;
        while duplicate.len() > 0 {
            result += 1;
            for _ in 0..3 {
                let num: &i32 = &nums[index];
                index += 1;
                counter.entry(*num).and_modify(|amount| *amount -= 1);
                if *counter.get(num).unwrap() == 1 && duplicate.contains(num) {
                    duplicate.remove(num);
                }

                if duplicate.len() == 0 || index >= n {
                    break;
                }
            }
        }

        return result
    }
}
```
