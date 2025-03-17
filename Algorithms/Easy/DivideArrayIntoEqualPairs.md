![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2206. [Divide Array Into Equal Pairs](https://leetcode.com/problems/divide-array-into-equal-pairs)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn divide_array(nums: Vec<i32>) -> bool {
        let mut counter: HashMap<i32, usize> = HashMap::new();
        for num in nums {
            counter.entry(num).and_modify(|num| *num += 1).or_insert(1);
        }

        return counter.values().filter(|amount| *amount % 2 != 0).collect::<Vec<_>>().len() == 0
    }
}
```

Method 2 (Hash Map + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn divide_array(nums: Vec<i32>) -> bool {
        let mut counter: HashMap<i32, usize> = HashMap::new();
        for num in nums {
            counter.entry(num).and_modify(|num| *num += 1).or_insert(1);
        }

        for amount in counter.values() {
            if amount % 2 == 1 {
                return false
            }
        }

        return true
    }
}
```
