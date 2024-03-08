![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Sqrt(x)](https://leetcode.com/problems/sqrtx)

### Solution :

Method 1 (the value of lower will fit answer when upper <= lower + 1, because $lower^2$ <= x and $(lower + 1)^2$ > x) :
```rust
use std::cmp::Ordering;
impl Solution {
    pub fn my_sqrt(x: i32) -> i32 {
        if x < 2 {
          return x
        }

        let mut lower = 0;
        let mut upper = x;
        while upper > lower + 1 {
            let mid = lower + (upper - lower) / 2;

            match mid.cmp(&(x / mid)) {
                Ordering::Less => lower = mid,
                Ordering::Greater => upper = mid,
                Ordering::Equal => {
                    return mid;
                },
            };
        }

        lower
    }
}
```

Method 2  (use standard function doesn't fit the description of problem) :
```rust
impl Solution {
    pub fn my_sqrt(x: i32) -> i32 {
        f64::sqrt(x as f64) as _
    }
}
```
