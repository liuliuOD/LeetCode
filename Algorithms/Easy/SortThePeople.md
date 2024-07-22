![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2418. [Sort The People](https://leetcode.com/problems/sort-the-people)

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn sort_people(names: Vec<String>, heights: Vec<i32>) -> Vec<String> {
        let n: usize = names.len();
        let mut index_ordered: Vec<usize> = (0..n).collect();
        /* Option 1 */
        index_ordered.sort_by_key(|&index| heights[index]);
        /* Option 2

        index_ordered.sort_unstable_by_key(|&index| heights[index]);
        */
        return index_ordered.iter().map(|&index| names[index].clone()).rev().collect()
    }
}
```

Method 2 (Built-In method, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;

impl Solution {
    pub fn sort_people(names: Vec<String>, heights: Vec<i32>) -> Vec<String> {
        return heights
            .iter()
            .map(Reverse)
            .zip(names.into_iter())
            .collect::<BinaryHeap<(Reverse<&i32>, String)>>()
            .into_sorted_vec()
            .into_iter()
            .map(|(_, name)| name)
            .collect()
    }
}
```

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sortPeople(self, names: List[str], heights: List[int]) -> List[str]:
        n = len(names)
        index_ordered = sorted(range(n), key=lambda index: heights[index], reverse=True)

        return [names[index] for index in index_ordered]
```
