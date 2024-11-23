![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1072. [Flip Columns For Maximum Number Of Equal Rows](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M*N)$, Space Complexity: $O(M)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
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

Method 2 (Hash Set, Time Complexity: $O(M*(M+N))$, Space Complexity: $O(M)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn max_equal_rows_after_flips(matrix: Vec<Vec<i32>>) -> i32 {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut visited: HashSet<usize> = HashSet::new();
        let mut result: i32 = 0;
        for index_m in 0..m {
            if visited.contains(&index_m) {
                continue;
            }

            let mut row_flip: Vec<i32> = Vec::with_capacity(n);
            for &element in matrix[index_m].iter() {
                row_flip.push(1-element);
            }

            let mut amount: i32 = 1;
            for index_m_next in index_m+1..m {
                if matrix[index_m_next].eq(&matrix[index_m]) || matrix[index_m_next].eq(&row_flip) {
                    visited.insert(index_m_next);
                    amount += 1;
                }
            }

            result = i32::max(result, amount);
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M*N)$, Space Complexity: $O(M)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```java
import java.util.HashMap;

class Solution {
    public int maxEqualRowsAfterFlips(int[][] matrix) {
        int n = matrix[0].length;
        HashMap<String, Integer> counter = new HashMap();
        int result = 0;
        for (int[] row: matrix) {
            StringBuilder key_builder = new StringBuilder();
            for (int index=1; index<n; index++) {
                if (row[index] != row[index-1]) {
                    key_builder.append('1');
                } else {
                    key_builder.append('0');
                }
            }

            String key = key_builder.toString();
            if (!counter.containsKey(key)) {
                counter.put(key, 1);
            } else {
                counter.replace(key, counter.get(key) + 1);
            }

            result = Math.max(result, counter.get(key));
        }

        return result;
    }
}
```
