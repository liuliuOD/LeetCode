![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3066. [Minimum Operations To Exceed Threshold Value II](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    pub fn min_operations(nums: Vec<i32>, k: i32) -> i32 {
        let mut min_heap: BinaryHeap<Reverse<i64>> = BinaryHeap::from(nums.into_iter().map(|num| Reverse(num as i64)).collect::<Vec<Reverse<i64>>>());
        let mut result: i32 = 0;
        while min_heap.len() >= 2 {
            let Reverse(first) = min_heap.pop().unwrap();
            if first >= k as i64 {
                break;
            }

            let Reverse(second) = min_heap.pop().unwrap();
            min_heap.push(Reverse(first*2+second));
            result += 1;
        }

        return result
    }
}
```
