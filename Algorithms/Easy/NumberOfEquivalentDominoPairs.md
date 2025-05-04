![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1128. [Number Of Equivalent Domino Pairs](https://leetcode.com/problems/number-of-equivalent-domino-pairs)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 18/19, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `dominoes`)) :
```rust
impl Solution {
    pub fn num_equiv_domino_pairs(dominoes: Vec<Vec<i32>>) -> i32 {
        let mut result: i32 = 0;
        let n: usize = dominoes.len();
        for index_i in 0..n {
            for index_j in index_i+1..n {
                if (dominoes[index_i][0] == dominoes[index_j][0] && dominoes[index_i][1] == dominoes[index_j][1]) || (dominoes[index_i][0] == dominoes[index_j][1] && dominoes[index_i][1] == dominoes[index_j][0]) {
                    result += 1;
                }
            }
        }

        return result
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `dominoes`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn num_equiv_domino_pairs(dominoes: Vec<Vec<i32>>) -> i32 {
        let n: usize = dominoes.len();
        let mut candidates: HashMap<(i32, i32), i32> = HashMap::new();
        let mut result: i32 = 0;
        for index in 0..n {
            result += *candidates.entry((dominoes[index][0], dominoes[index][1])).or_default();
            if dominoes[index][0] != dominoes[index][1] {
                result += *candidates.entry((dominoes[index][1], dominoes[index][0])).or_default();
            }

            candidates.entry((dominoes[index][0], dominoes[index][1])).and_modify(|amount| *amount += 1).or_insert(1);
        }

        return result
    }
}
```
