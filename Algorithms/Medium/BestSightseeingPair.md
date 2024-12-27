![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1014. [Best Sightseeing Pair](https://leetcode.com/problems/best-sightseeing-pair)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M*N)$, Space Complexity: $O(M)$ (M: the range of the value in `values`, N: the number of the elements in `values`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn max_score_sightseeing_pair(values: Vec<i32>) -> i32 {
        let mut mapping: HashMap<i32, usize> = HashMap::from([(values[0], 0)]);
        let mut result: i32 = i32::MIN;
        for index in 1..values.len() {
            let current: i32 = values[index];
            for (&num, &index_num) in &mapping {
                result = i32::max(result, current + num + index_num as i32 - index as i32);
            }

            mapping.entry(current).and_modify(|item| *item = index).or_insert(index);
        }

        return result
    }
}
```
