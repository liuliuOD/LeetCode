![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Sign Of The Product Of An Array](https://leetcode.com/problems/sign-of-the-product-of-an-array)

### Solution :

Method 1 :
```rust
use std::cmp::Ordering;
impl Solution {
    pub fn array_sign(nums: Vec<i32>) -> i32 {
        let mut result = 1;
        for i in nums {
            match i.cmp(&0) {
                Ordering::Equal => result *= 0,
                Ordering::Greater => result *= 1,
                Ordering::Less => result *= -1,
            };
        }

        result
    }
}
```
