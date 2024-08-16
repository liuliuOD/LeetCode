![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 624. [Maximum Distance In Arrays](https://leetcode.com/problems/maximum-distance-in-arrays)

### Solution :

Method 1 (Binary Heap) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;

impl Solution {
    pub fn max_distance(arrays: Vec<Vec<i32>>) -> i32 {
        let n: usize = arrays.len();
        let mut minimums: Vec<i32> = Vec::with_capacity(n);
        let mut maximums: Vec<i32> = Vec::with_capacity(n);
        let mut minimum_top_2: BinaryHeap<i32> = BinaryHeap::new();
        let mut maximum_top_2: BinaryHeap<Reverse<i32>> = BinaryHeap::new();
        for array in arrays {
            /* Option 1 */
            let minimum: i32 = *array.iter().min().unwrap();
            let maximum: i32 = *array.iter().max().unwrap();
            /* Option 2

            let minimum: i32 = array[0];
            let maximum: i32 = *array.last().unwrap();
            */
            minimums.push(minimum);
            maximums.push(maximum);

            minimum_top_2.push(minimum);
            maximum_top_2.push(Reverse(maximum));

            if minimum_top_2.len() > 2 {
                minimum_top_2.pop();
            }
            if maximum_top_2.len() > 2 {
                maximum_top_2.pop();
            }
        }

        let sorted_minimum_top_2: Vec<i32> = minimum_top_2.into_sorted_vec();
        let sorted_maximum_top_2: Vec<Reverse<i32>> = maximum_top_2.into_sorted_vec();
        let mut result: i32 = 0;
        for index in 0..n {
            let mut minimum: i32 = minimums[index];
            let mut maximum: i32 = maximums[index];
            if let Reverse(value) = sorted_maximum_top_2[0] {
                if value != maximum {
                    maximum = value;
                    continue;
                }

                match sorted_maximum_top_2[1] {
                    Reverse(value) => {
                        maximum = value;
                    },
                    _ => {},
                }
            }

            result = result.max((maximum-minimum).abs());

            maximum = maximums[index];
            if sorted_minimum_top_2[0] == minimum {
                minimum = sorted_minimum_top_2[1];
            } else {
                minimum = sorted_minimum_top_2[0];
            }

            result = result.max((maximum-minimum).abs());
        }

        return result
    }
}
```
