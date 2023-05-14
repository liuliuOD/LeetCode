![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2679. [Sum In A Matrix](https://leetcode.com/problems/sum-in-a-matrix)

### Solution :

Method 1 (Binary Heap to handle largest) :
```rust
use std::cmp::max;
use std::collections::BinaryHeap;
impl Solution {
    pub fn matrix_sum(nums: Vec<Vec<i32>>) -> i32 {
        let mut heap_rows = vec![BinaryHeap::new(); nums.len()];
        for i in 0..nums.len() {
            for j in 0..nums[0].len() {
                heap_rows[i].push((nums[i][j]));
            }
        }

        let mut result = 0;
        while !heap_rows[0].is_empty() {
            let mut temp = i32::MIN;
            for i in 0..nums.len() {
                temp = max(temp, heap_rows[i].pop().unwrap());
            }
            result += temp;
        }
        
        result
    }
}
```
