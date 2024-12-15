![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1792. [Maximum Average Pass Ratio](https://leetcode.com/problems/maximum-average-pass-ratio)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O((M+N)*Log(N))$, Space Complexity: $O(N)$ (M: the value of `extra_students`, N: the number of the elements in `classes`)) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Ordering;

#[derive(Debug, PartialEq, PartialOrd)]
struct ComparableF64(f64);

impl Eq for ComparableF64 {}

impl Ord for ComparableF64 {
    fn cmp(&self, other: &Self) -> Ordering {
        self.partial_cmp(other)
            .unwrap_or_else(|| if self.0.is_nan() { Ordering::Less } else { Ordering::Greater })
    }
}

impl Solution {
    pub fn max_average_ratio(classes: Vec<Vec<i32>>, extra_students: i32) -> f64 {
        let n: usize = classes.len();
        let mut heap: BinaryHeap<(ComparableF64, i32, i32)> = BinaryHeap::from_iter(classes.into_iter().map(|item| {
            let mut ratio: ComparableF64 = ComparableF64(0.0);
            if item[0] != item[1] {
                ratio = ComparableF64(((item[0]+1) as f64 / (item[1]+1) as f64) - (item[0] as f64 / item[1] as f64));
            }

            return (ratio, item[0], item[1])
        }));

        for _ in 0..extra_students {
            let (_, pass, total) = heap.pop().unwrap();
            heap.push((ComparableF64(((pass+2) as f64 / (total+2) as f64) - ((pass+1) as f64 / (total+1) as f64)), pass+1, total+1));
        }

        let mut result: f64 = 0.0;
        while heap.len() > 0 {
            let (_, pass, total) = heap.pop().unwrap();
            result += pass as f64 / total as f64;
        }

        return result / n as f64
    }
}
```
