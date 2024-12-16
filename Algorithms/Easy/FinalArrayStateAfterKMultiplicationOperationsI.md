![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3264. [Final Array State After K Multiplication Operations I](https://leetcode.com/problems/final-array-state-after-k-multiplication-operations-i)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O((N+K)*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`, K: the value of `k`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    pub fn get_final_state(mut nums: Vec<i32>, k: i32, multiplier: i32) -> Vec<i32> {
        let mut heap: BinaryHeap<(Reverse<i32>, Reverse<usize>)> = BinaryHeap::from_iter(nums.iter().enumerate().map(|(index, &num)| (Reverse(num), Reverse(index))));
        for _ in 0..k {
            let (Reverse(num), Reverse(index)) = heap.pop().unwrap();
            nums[index] *= multiplier;
            heap.push((Reverse(nums[index]), Reverse(index)));
        }

        return nums
    }
}
```
