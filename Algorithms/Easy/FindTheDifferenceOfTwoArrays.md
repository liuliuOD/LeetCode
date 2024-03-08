![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Find The Difference Of Two Arrays](https://leetcode.com/problems/find-the-difference-of-two-arrays)

### Solution :

Method 1 :
```rust
use std::collections::HashSet;
use std::iter::FromIterator;
impl Solution {
    pub fn find_difference(mut nums1: Vec<i32>, mut nums2: Vec<i32>) -> Vec<Vec<i32>> {
        let hs1 = nums1.into_iter().collect::<HashSet<i32>>();
        // or
        let hs2: HashSet<i32> = HashSet::from_iter(nums2);

        let mut result = vec![];
        result.push(hs1.difference(&hs2).cloned().collect());
        result.push(hs2.difference(&hs1).cloned().collect());

        result
    }
}
```

Method 2 :
```rust
use std::collections::HashSet;
use std::iter::FromIterator;
impl Solution {
    pub fn find_difference(mut nums1: Vec<i32>, mut nums2: Vec<i32>) -> Vec<Vec<i32>> {
        let hs1: HashSet<i32> = HashSet::from_iter(nums1);
        let hs2: HashSet<i32> = HashSet::from_iter(nums2);

        vec![
            hs1.difference(&hs2).copied().collect(),
            hs2.difference(&hs1).copied().collect(),
        ]
    }
}
```
