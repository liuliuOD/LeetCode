![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2906. [Construct Product Matrix](https://leetcode.com/problems/construct-product-matrix)

### Solution :

Method 1 (Prefix Sum + Suffix Sum) :
```python
MODULO = 12345
class Solution:
    def constructProductMatrix(self, grid: List[List[int]]) -> List[List[int]]:
        m = len(grid)
        n = len(grid[0])
        result = [[1] * n for _ in range(m)]

        # Prefix
        product = 1
        for index_m in range(m):
            for index_n in range(n):
                result[index_m][index_n] = result[index_m][index_n] * product % MODULO
                product = product * grid[index_m][index_n] % MODULO

        # Suffix
        product = 1
        for index_m in reversed(range(m)):
            for index_n in reversed(range(n)):
                result[index_m][index_n] = result[index_m][index_n] * product % MODULO
                product = product * grid[index_m][index_n] % MODULO

        return result
```

Method 2 (Prefix Sum + Suffix Sum) :
```python
MODULO = 12345
class Solution:
    def constructProductMatrix(self, grid: List[List[int]]) -> List[List[int]]:
        m = len(grid)
        n = len(grid[0])
        result = [[1] * n for _ in range(m)]

        # Prefix
        self.multiply(range(m), range(n), result, grid)

        # Suffix
        # Hint: can't use reversed(range(m)) and reversed(range(n)), this may occur unexpected result
        self.multiply(range(m-1, -1, -1), range(n-1, -1, -1), result, grid)

        return result

    def multiply(self, range_m, range_n, result, grid):
        product = 1
        for index_m in range_m:
            for index_n in range_n:
                result[index_m][index_n] = result[index_m][index_n] * product % MODULO
                product = product * grid[index_m][index_n] % MODULO
```
