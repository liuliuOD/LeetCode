![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Average Salary Excluding The Minimum And Maximum Salary](https://leetcode.com/problems/average-salary-excluding-the-minimum-and-maximum-salary)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn average(salary: Vec<i32>) -> f64 {
        let mut minimum = i32::MAX;
        let mut maximum = 0;
        let mut sum:f64 = 0.0;
        for &amount in &salary {
            if amount < minimum {
                minimum = amount;
            }

            if amount > maximum {
                maximum = amount;
            }

            sum += amount as f64;
        }

        (sum - (minimum + maximum) as f64) / ((salary.clone().len() - 2) as f64)
    }
}
```

Method 2 :
```rust
use std::cmp;
impl Solution {
    pub fn average(salary: Vec<i32>) -> f64 {
        let mut minimum = i32::MAX;
        let mut maximum = 0;
        let mut sum:f64 = 0.0;
        for &amount in &salary {
            minimum = cmp::min(minimum, amount);
            maximum = cmp::max(maximum, amount);

            sum += amount as f64;
        }

        (sum - (minimum + maximum) as f64) / ((salary.clone().len() - 2) as f64)
    }
}
```
