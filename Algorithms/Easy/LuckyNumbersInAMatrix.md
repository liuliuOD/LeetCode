![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1380. [Lucky Numbers In A Matrix](https://leetcode.com/problems/lucky-numbers-in-a-matrix)

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$ (M: the numbers of the elements in `matrix`, N: the numbers of the elements in `matrix[0]`)) :
```rust
impl Solution {
    pub fn lucky_numbers (matrix: Vec<Vec<i32>>) -> Vec<i32> {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut maximum_columns: Vec<i32> = Vec::with_capacity(n);
        for _ in 0..n {
            maximum_columns.push(i32::MIN);
        }
        let mut minimum_rows: Vec<(i32, usize)> = Vec::with_capacity(m);
        for index_m in 0..m {
            let mut minimum_index: usize = 0;
            let mut minimum_value: i32 = i32::MAX;
            for index_n in 0..n {
                let value: i32 = matrix[index_m][index_n];
                if value < minimum_value {
                    minimum_value = value;
                    minimum_index = index_n;
                }

                maximum_columns[index_n] = maximum_columns[index_n].max(value);
            }

            minimum_rows.push((minimum_value, minimum_index));
        }

        let mut result: Vec<i32> = Vec::new();
        for index_m in 0..m {
            let (value, index_n) = minimum_rows[index_m];
            if value == maximum_columns[index_n] {
                result.push(value);
            }
        }

        return result
    }
}
```
