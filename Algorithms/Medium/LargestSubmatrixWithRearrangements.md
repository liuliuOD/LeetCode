![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1727. [Largest Submatrix With Rearrangements](https://leetcode.com/problems/largest-submatrix-with-rearrangements)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn largest_submatrix(mut matrix: Vec<Vec<i32>>) -> i32 {
        let mut result: i32 = 0;
        for index_x in 0..matrix.len() {
            if index_x > 0 {
                for index_y in 0..matrix[index_x].len() {
                    if matrix[index_x][index_y] == 0 {
                        continue;
                    }

                    matrix[index_x][index_y] += matrix[index_x-1][index_y];
                }
            }

            let mut row: Vec<i32> = matrix[index_x].clone();
            row.sort();
            row.reverse();
            for index in 0..row.len() {
                result = result.max(row[index]*(1+index as i32));
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N*Log(N))$, Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language)) :
```python
class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        for index_x in range(1, m):
            for index_y in range(n):
                if matrix[index_x][index_y] <= 0:
                    continue

                matrix[index_x][index_y] += matrix[index_x-1][index_y]

        result = 0
        for row in matrix:
            # Option 1
            row.sort(reverse=True)
            minimum = inf
            for index in range(n):
                minimum = min(minimum, row[index])
                result = max(result, minimum*(index+1))
            """
            # Option 2

            for index, item in enumerate(sorted(row, reverse=True)):
                result = max(result, item*(index+1))
            """

        return result
```

Method 2 :
```python
class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        result = 0
        for index_x in range(m):
            if index_x > 0:
                for index_y in range(n):
                    if matrix[index_x][index_y] <= 0:
                        continue

                    matrix[index_x][index_y] += matrix[index_x-1][index_y]

            for index, item in enumerate(sorted(matrix[index_x], reverse=True)):
                result = max(result, item*(index+1))

        return result
```
