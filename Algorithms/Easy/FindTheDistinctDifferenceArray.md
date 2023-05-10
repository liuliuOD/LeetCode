![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Find The Distinct Difference Array](https://leetcode.com/problems/find-the-distinct-difference-array)

### Solution :

Method 1 (In weekly contest 344, Brute Force) :
```rust
impl Solution {
    pub fn distinct_difference_array(nums: Vec<i32>) -> Vec<i32> {
        let mut result = vec![];
        let mut left = vec![];
        let mut right = vec![];
        for i in 0..nums.len() {
            left = nums.clone()[0..i+1].to_vec();
            right = nums.clone()[i+1..nums.len()].to_vec();
            
            left.sort();
            right.sort();
            left.dedup();
            right.dedup();
            result.push((left.len() - right.len()) as i32);
        }
        result
    }
}
```
