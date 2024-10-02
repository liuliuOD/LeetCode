![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1331. [Rank Transform Of An Array](https://leetcode.com/problems/rank-transform-of-an-array)

### Solution :

Method 1 (Hash Map + Hash Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `arr`)) :
```rust
use std::collections::{HashSet, HashMap};

impl Solution {
    pub fn array_rank_transform(arr: Vec<i32>) -> Vec<i32> {
        let mut unique: Vec<&i32> = Vec::from_iter(arr.iter().collect::<HashSet<&i32>>().into_iter());
        unique.sort();
        let ranking: HashMap<i32, usize> = unique.into_iter().enumerate().map(|(index, &value)| (value, index+1)).collect();

        let mut result: Vec<i32> = Vec::new();
        for item in arr.iter() {
            result.push(ranking[item] as i32);
        }

        return result
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `arr`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn array_rank_transform(arr: Vec<i32>) -> Vec<i32> {
        let mut unique: Vec<i32> = arr.clone();
        unique.sort_unstable();
        unique.dedup();
        let ranking: HashMap<i32, i32> = unique.into_iter().enumerate().map(|(index, value)| (value, index as i32 + 1)).collect();

        let n: usize = arr.len();
        let mut result: Vec<i32> = Vec::with_capacity(n);
        for item in arr.iter() {
            result.push(ranking[item]);
        }

        return result
    }
}
```
