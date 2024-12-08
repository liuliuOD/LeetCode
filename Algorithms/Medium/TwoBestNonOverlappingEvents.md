![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2054. [Two Best Non-Overlapping Events](https://leetcode.com/problems/two-best-non-overlapping-events)

### Solution :

Method 1 (Array Sorted + Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `events`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    pub fn max_two_events(events: Vec<Vec<i32>>) -> i32 {
        let n: usize = events.len();
        let mut heap: BinaryHeap<(Reverse<i32>, i32)> = BinaryHeap::new();
        let mut events_sorted: Vec<usize> = (0..n).collect();
        events_sorted.sort_by_key(|&index| events[index][0]);
        let mut maximum: i32 = 0;
        let mut result: i32 = 0;
        for index in events_sorted {
            while heap.len() > 0 {
                /* Option 1 */
                if let Reverse(end) = heap.peek().unwrap().0 {
                    if end >= events[index][0] {
                        break;
                    }

                }
                /* Option 2

                let Reverse(end) = heap.peek().unwrap().0;
                if end >= events[index][0] {
                    break;
                }
                */

                let item: (Reverse<i32>, i32) = heap.pop().unwrap();
                maximum = i32::max(maximum, item.1);
            }
            heap.push((Reverse(events[index][1]), events[index][2]));

            result = i32::max(result, maximum + events[index][2]);
        }

        return result
    }
}
```
