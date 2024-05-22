![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 48. [Rotate Image](https://leetcode.com/problems/rotate-image)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        # reverse along the diagonal
        for index_row in range(n):
            for index_column in range(index_row+1, n):
                matrix[index_row][index_column], matrix[index_column][index_row] = matrix[index_column][index_row], matrix[index_row][index_column]

        # reverse along the center line of x-axis
        for index_row in range(n):
            for index_column in range(n//2):
                matrix[index_row][index_column], matrix[index_row][n-1-index_column] = matrix[index_row][n-1-index_column], matrix[index_row][index_column]
```

Method 2 (Using Built-In Method) :
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        # reverse along the diagonal
        for index_row in range(n):
            for index_column in range(index_row+1, n):
                matrix[index_row][index_column], matrix[index_column][index_row] = matrix[index_column][index_row], matrix[index_row][index_column]

        # reverse along the center line of x-axis
        for row in matrix:
            row.reverse()
```
