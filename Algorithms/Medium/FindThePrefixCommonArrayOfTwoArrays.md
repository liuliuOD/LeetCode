![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Find The Prefix Common Array Of Two Arrays](https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays)

### Solution :

Method 1 (In biweekly contest 103, Brute Force) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn find_the_prefix_common_array(a: Vec<i32>, b: Vec<i32>) -> Vec<i32> {
        let n = a.len();
        let mut result = vec![0; n];
        let mut hs_A = HashSet::new();
        let mut hs_B = HashSet::new();
        
        let mut contain = HashSet::new();
        for i in 0..n {            
            hs_A.insert(a[i]);
            hs_B.insert(b[i]);

            for j in 0..i+1 {
                if hs_A.contains(&a[j]) && hs_B.contains(&a[j]) {
                    contain.insert(a[j]);
                }
                if hs_A.contains(&b[j]) && hs_B.contains(&b[j]) {
                    contain.insert(b[j]);
                }
            }
            result[i] += contain.len() as i32;
        }
        
        result
    }
}
```
