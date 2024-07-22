![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
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

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `row_sum`, N: the number of the elements in `col_sum`)) :
```python
class Solution:
    def restoreMatrix(self, row_sum: List[int], col_sum: List[int]) -> List[List[int]]:
        m = len(row_sum)
        n = len(col_sum)
        result = [[0]*n for _ in range(m)]
        for index_m in range(m):
            for index_n in range(n):
                current = min(row_sum[index_m], col_sum[index_n])
                result[index_m][index_n] = current
                row_sum[index_m] -= current
                col_sum[index_n] -= current

        return result
```

Method 2 (Greedy + Time Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `row_sum`, N: the number of the elements in `col_sum`)) :
```python
class Solution:
    def restoreMatrix(self, row_sum: List[int], col_sum: List[int]) -> List[List[int]]:
        m = len(row_sum)
        n = len(col_sum)
        result = [[0]*n for _ in range(m)]
        index_m = index_n = 0
        while index_m < m and index_n < n:
            current = min(row_sum[index_m], col_sum[index_n])
            result[index_m][index_n] = current
            row_sum[index_m] -= current
            col_sum[index_n] -= current

            if row_sum[index_m] == 0:
                index_m += 1
            else:
                index_n += 1

        return result
```
