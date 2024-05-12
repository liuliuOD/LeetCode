![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2373. [Largest Local Values In A Matrix](https://leetcode.com/problems/largest-local-values-in-a-matrix)

### Solution :

Method 1 (Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def largestLocal(self, grid: List[List[int]]) -> List[List[int]]:
        m, n = len(grid), len(grid[0])
        maximum_m = [[max(grid[index_m][index_n_start:index_n_start+3]) for index_n_start in range(n-3+1)] for index_m in range(m)]

        # Option 1
        result = [[0]*(n-2) for _ in range(m-2)]
        for index_m in range(m-2):
            for index_n in range(n-2):
                result[index_m][index_n] = max(maximum_m[index_m_current][index_n] for index_m_current in range(index_m, index_m+3))

        return result
        """
        # Option 2

        return [[max(maximum_m[index_m_current][index_n] for index_m_current in range(index_m, index_m+3)) for index_n in range(n-2)] for index_m in range(m-2)]
        """
```

Method 2 (Built-In method, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def largestLocal(self, grid: List[List[int]]) -> List[List[int]]:
        m, n = len(grid), len(grid[0])
        return [[max(max(grid[index_m+offset][index_n:index_n+3]) for offset in range(3)) for index_n in range(n-2)] for index_m in range(m-2)]
```
