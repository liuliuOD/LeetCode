![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1072. [Flip Columns For Maximum Number Of Equal Rows](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M*N)$, Space Complexity: $O(M)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn max_equal_rows_after_flips(matrix: Vec<Vec<i32>>) -> i32 {
        let mut mapping: HashMap<String, i32> = HashMap::new();
        let mut result: i32 = 0;
        for row in matrix {
            let mut key: String = String::new();
            for index in 1..row.len() {
                if row[index] == row[index-1] {
                    key.push_str("0");
                } else {
                    key.push_str("1");
                }
            }

            mapping.entry(key.clone()).and_modify(|value| *value += 1).or_insert(1);
            result = i32::max(result, *mapping.get(&key).unwrap());
        }

        return result
    }
}
```
