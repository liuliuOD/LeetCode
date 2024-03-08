![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3070. [Count Submatrices With Top-Left Element And Sum Less Than K](https://leetcode.com/problems/count-submatrices-with-top-left-element-and-sum-less-than-k)

### Solution :

Method 1 (In weekly contest 387, Prefix Sum, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def countSubmatrices(self, grid: List[List[int]], k: int) -> int:
        m = len(grid)
        n = len(grid[0])
        prefix_sum = [[0]*(n+1) for _ in range(m+1)]
        for index_m in range(m):
            for index_n in range(n):
                prefix_sum[index_m+1][index_n+1] = grid[index_m][index_n] + prefix_sum[index_m+1][index_n] + prefix_sum[index_m][index_n+1] - prefix_sum[index_m][index_n]

        result = 0
        for index_m in range(1, m+1):
            for index_n in range(1, n+1):
                if prefix_sum[index_m][index_n] <= k:
                    result += 1

        return result
```
