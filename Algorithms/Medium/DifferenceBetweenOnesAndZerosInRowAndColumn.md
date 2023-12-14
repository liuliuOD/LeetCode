![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2482. [Difference Between Ones And Zeros In Row And Column](https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn ones_minus_zeros(grid: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut row_one: Vec<i32> = vec![0; m];
        let mut column_one: Vec<i32> = vec![0; n];
        for index_m in 0..m {
            for index_n in 0..n {
                if grid[index_m][index_n] == 1 {
                    row_one[index_m] += 1;
                    column_one[index_n] += 1;
                }
            }
        }

        let mut result: Vec<Vec<i32>> = vec![vec![0; n]; m];
        for index_m in 0..m {
            for index_n in 0..n {
                result[index_m][index_n] = row_one[index_m]*2 + column_one[index_n]*2 - m as i32 - n as i32;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$) :
```python
class Solution:
    def onesMinusZeros(self, grid: List[List[int]]) -> List[List[int]]:
        m = len(grid)
        n = len(grid[0])
        row_one = [sum(row) for row in grid]
        column_one = [sum([grid[index_m][index_n] for index_m in range(m)]) for index_n in range(n)]
        row_zero = [row.count(0) for row in grid]
        column_zero = [[grid[index_m][index_n] for index_m in range(m)].count(0) for index_n in range(n)]

        result = []
        for index_m in range(m):
            temp = []
            for index_n in range(n):
                temp.append(row_one[index_m]+column_one[index_n]-row_zero[index_m]-column_zero[index_n])

            result.append(temp)

        return result
```

Method 2 (Clean Code) :
```python
class Solution:
    def onesMinusZeros(self, grid: List[List[int]]) -> List[List[int]]:
        m = len(grid)
        n = len(grid[0])
        row_one = [sum(row) for row in grid]
        column_one = [sum([grid[index_m][index_n] for index_m in range(m)]) for index_n in range(n)]

        # Option 1
        result = []
        for index_m in range(m):
            temp = []
            for index_n in range(n):
                """
                row_one + column_one - (m-row_one) - (n-column_one) = row_one * 2 + column_one * 2 - m - n
                """
                temp.append(row_one[index_m]*2+column_one[index_n]*2-m-n)

            result.append(temp)

        return result
        """
        # Option 2

        return [[row_one[index_m]*2+column_one[index_n]*2-m-n for index_n in range(n)] for index_m in range(m)]
        """
```
