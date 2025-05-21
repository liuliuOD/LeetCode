![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 73. [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N^2*M)$, Space Complexity: $O(N+M)$ (N: the number of the elements in `matrix`, m: the number of the elements in `matrix[0]`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn set_zeroes(matrix: &mut Vec<Vec<i32>>) {
        let n: usize = matrix.len();
        let m: usize = matrix[0].len();
        let mut zero_row: HashSet<usize> = HashSet::new();
        let mut zero_column: HashSet<usize> = HashSet::new();
        for index_n in 0..n {
            for index_m in 0..m {
                if matrix[index_n][index_m] != 0 {
                    continue;
                }

                zero_row.insert(index_n);
                zero_column.insert(index_m);
            }
        }

        for index_n in 0..n {
            if !zero_row.contains(&index_n) {
                continue;
            }

            for index_m in 0..m {
                matrix[index_n][index_m] = 0;

                if !zero_column.contains(&index_m) {
                    continue;
                }

                for index_n_zero in 0..n {
                    matrix[index_n_zero][index_m] = 0;
                }
            }
        }
    }
}
```

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        m = len(matrix)
        n = len(matrix[0])
        positions = []
        for index_row in range(m):
            for index_column in range(n):
                if matrix[index_row][index_column] != 0:
                    continue

                positions.append((index_row, index_column))

        while positions:
            x, y = positions.pop()
            for index_row in range(m):
                matrix[index_row][y] = 0

            # Option 1
            for index_column in range(n):
                matrix[x][index_column] = 0
            """
            # Option 2
            matrix[x] = [0] * n
            """
```
