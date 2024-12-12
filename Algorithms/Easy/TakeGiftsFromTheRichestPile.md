![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2558. [Take Gifts From The Richest Pile](https://leetcode.com/problems/take-gifts-from-the-richest-pile)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*Log(N)+N*Log(N))$, Space Complexity: $O(N)$ (M: the value of `k`, N: the number of the elements in `gifts`)) :
```Rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn pick_gifts(gifts: Vec<i32>, k: i32) -> i64 {
        let mut heap: BinaryHeap<i64> = BinaryHeap::from_iter(gifts.into_iter().map(|num| num as i64));
        for _ in 0..k {
            if let Some(num) = heap.pop() {
                heap.push((num as f64).sqrt() as i64);
            }
        }

        return heap.into_iter().sum()
    }
}
```
