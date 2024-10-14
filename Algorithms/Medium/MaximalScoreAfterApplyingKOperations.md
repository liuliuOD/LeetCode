![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2530. [Maximal Score After Applying K Operations](https://leetcode.com/problems/maximal-score-after-applying-k-operations)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N)+K*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`, K: the value of `k`)) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn max_kelements(nums: Vec<i32>, k: i32) -> i64 {
        let mut heap: BinaryHeap<i32> = BinaryHeap::new();
        for num in nums {
            heap.push(num);
        }

        let mut result: i64 = 0;
        for _ in 0..k {
            let mut maximum: i32 = heap.pop().unwrap();
            result += maximum as i64;

            heap.push((maximum + 3 - 1) / 3);
        }

        return result
    }
}
```
