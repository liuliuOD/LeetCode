![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Maximum Sum With Exactly K Elements](https://leetcode.com/problems/maximum-sum-with-exactly-k-elements)

### Solution :

Method 1 (In biweekly contest 103) :
```rust
impl Solution {
    pub fn maximize_sum(nums: Vec<i32>, k: i32) -> i32 {
        let mut choosen = 0;
        for item in nums {
            if item > choosen {
                choosen = item;
            }
        }
        
        (0..k).into_iter().sum::<i32>() + choosen*k
    }
}
```
