![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1405. [Longest Happy String](https://leetcode.com/problems/longest-happy-string)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(A+B+C)$, Space Complexity: $O(1)$ (A: the value of `a`, B: the value of `b`, C: the value of `c`)) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn longest_diverse_string(a: i32, b: i32, c: i32) -> String {
        let mut heap: BinaryHeap<(i32, u8)> = BinaryHeap::from([(a, b'a'), (b, b'b'), (c, b'c')]);
        let mut amount_accumulative: i32 = 0;
        let mut result: Vec<u8> = Vec::new();
        while heap.len() > 0 {
            let mut item: (i32, u8) = heap.pop().unwrap();
            if item.0 <= 0 {
                break;
            }

            if result.len() == 0 || *result.last().unwrap() != item.1 {
                amount_accumulative = 1;
            } else if *result.last().unwrap() == item.1 && amount_accumulative == 2 {
                if heap.len() == 0 {
                    break;
                }

                let mut item_second: (i32, u8) = heap.pop().unwrap();
                if item_second.0 <= 0 {
                    break;
                }

                heap.push(item);
                item = item_second;
                amount_accumulative = 1;
            } else {
                amount_accumulative += 1;
            }

            result.push(item.1);
            item.0 -= 1;
            heap.push(item);
        }

        return String::from_utf8(result).unwrap()
    }
}
```
