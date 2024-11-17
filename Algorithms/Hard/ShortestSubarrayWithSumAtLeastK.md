![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 862. [Shortest Subarray With Sum At Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    pub fn shortest_subarray(nums: Vec<i32>, k: i32) -> i32 {
        let k: i64 = k as i64;
        let mut heap: BinaryHeap<(Reverse<i64>, usize)> = BinaryHeap::new();
        let mut sum: i64 = 0;
        let mut result: i32 = i32::MAX;
        for index in 0..nums.len() {
            sum += nums[index] as i64;
            if sum >= k {
                result = i32::min(result, (index+1) as i32);
            }

            while !heap.is_empty() {
                if let Reverse(sum_previous) = heap.peek().unwrap().0 {
                    if sum-sum_previous < k {
                        break;
                    }

                    result = i32::min(result, (index-heap.pop().unwrap().1) as i32);
                }
            }

            heap.push((Reverse(sum), index));
        }

        return match result {
            i32::MAX => -1,
            result => result,
        }
    }
}
```
