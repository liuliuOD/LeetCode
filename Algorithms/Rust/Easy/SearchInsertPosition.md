![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Search Insert Position](https://leetcode.com/problems/search-insert-position)

### Solution :

Method 1 (time complexity: O(n)) :
```rust
impl Solution {
    pub fn search_insert(nums: Vec<i32>, target: i32) -> i32 {
        for i in 0..nums.len() {
            if nums[i] >= target {
                return i as i32
            }
        }

        nums.len() as i32
    }
}
```

Method 2 (use binary search, time complexity: O(log n)) :
```rust
use std::cmp::Ordering;

impl Solution {
    pub fn search_insert(nums: Vec<i32>, target: i32) -> i32 {
        let mut left = 0 as i32;
        let mut right = (nums.len() - 1) as i32;
        while left <= right {
            let middle = (left + right) / 2;

            match nums[middle as usize].cmp(&target) {
                Ordering::Equal => return middle,
                Ordering::Less => left = middle + 1,
                Ordering::Greater => right = middle - 1,
            }
        }

        left
    }
}
```

Method 3 (binary search in standard library, time complexity: O(log n)) :
```rust
use std::cmp::Ordering;

impl Solution {
    pub fn search_insert(nums: Vec<i32>, target: i32) -> i32 {
        match nums.binary_search(&target) {
            Ok(value) => value as _,
            Err(value) => value as _,
        }
    }
}
```
