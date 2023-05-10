![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii)

### Solution :

Method 1 (Sliding Window + HashMap) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn contains_nearby_duplicate(nums: Vec<i32>, k: i32) -> bool {
        let k = k as usize;
        let mut hm = HashMap::new();
        for (index, &num) in nums.iter().enumerate() {
            if index > k {
                *hm.entry(nums[index - k - 1]).or_insert(0) -= 1;
            }
            if *hm.get(&num).unwrap_or(&0) >= 1 {
                return true
            }

            *hm.entry(num).or_insert(0) += 1;
        }

        false
    }
}
```

Method 2 (Sliding Window + HashSet) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn contains_nearby_duplicate(nums: Vec<i32>, k: i32) -> bool {
        let k = k as usize;
        let mut hs = HashSet::new();
        for (index, &num) in nums.iter().enumerate() {
            if index > k {
                hs.remove(&nums[index - k - 1]);
            }
            if hs.contains(&num) {
                return true
            }

            hs.insert(num);
        }

        false
    }
}
```
