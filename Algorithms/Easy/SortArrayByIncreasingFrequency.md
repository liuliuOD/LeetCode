![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1636. [Sort Array By Increasing Frequency](https://leetcode.com/problems/sort-array-by-increasing-frequency)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::{BinaryHeap, HashMap};
impl Solution {
    pub fn frequency_sort(nums: Vec<i32>) -> Vec<i32> {
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for num in nums {
            mapping.entry(num).and_modify(|value| *value += 1).or_insert(1);
        }

        let mut counter: HashMap<i32, BinaryHeap<i32>> = HashMap::new();
        for (&key, &value) in mapping.iter() {
            counter.entry(value).and_modify(|heap| heap.push(key)).or_insert(BinaryHeap::from([key]));
        }

        let mut ordered: Vec<i32> = Vec::from_iter(counter.keys().map(|&value| value));
        ordered.sort();
        let mut result: Vec<i32> = Vec::new();
        for key in ordered {
            counter.entry(key).and_modify(|heap| {
                while !heap.is_empty() {
                    let num: i32 = heap.pop().unwrap();
                    for _ in 0..key {
                        result.push(num);
                    }
                }
            });
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::cmp::Reverse;
use std::collections::HashMap;
impl Solution {
    pub fn frequency_sort(mut nums: Vec<i32>) -> Vec<i32> {
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for num in nums.iter() {
            mapping.entry(*num).and_modify(|value| *value += 1).or_insert(1);
        }

        nums.sort_by_key(|num| (mapping[num], Reverse(*num)));
        return nums
    }
}
```
