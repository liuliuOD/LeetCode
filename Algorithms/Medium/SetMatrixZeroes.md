![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 73. [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes)

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
