![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1605. [Find Valid Matrix Given Row And Column Sums](https://leetcode.com/problems/find-valid-matrix-given-row-and-column-sums)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `row_sum`, N: the number of the elements in `col_sum`)) :
```rust
impl Solution {
    pub fn restore_matrix(row_sum: Vec<i32>, col_sum: Vec<i32>) -> Vec<Vec<i32>> {
        let m: usize = row_sum.len();
        let n: usize = col_sum.len();
        let mut current_row_sum: Vec<i32> = Vec::from_iter((0..m).map(|_| 0));
        let mut current_col_sum: Vec<i32> = Vec::from_iter((0..n).map(|_| 0));
        let mut result: Vec<Vec<i32>> = Vec::new();
        for index_m in 0..m {
            let mut row: Vec<i32> = Vec::with_capacity(n);
            for index_n in 0..n {
                let current_value: i32 = i32::min(row_sum[index_m] - current_row_sum[index_m], col_sum[index_n] - current_col_sum[index_n]);

                current_row_sum[index_m] += current_value;
                current_col_sum[index_n] += current_value;
                row.push(current_value);
            }

            result.push(row);
        }

        return result
    }
}
```
