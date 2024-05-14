![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1219. [Path With Maximum Gold](https://leetcode.com/problems/path-with-maximum-gold)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(M*N*4^P)$ (M: length of `grid`, N: length of `grid[0]`, P: value of $M*N$), Space Complexity: $O(4^P)$) :
```python
class Solution:
    def getMaximumGold(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        result = 0
        for index_m in range(m):
            for index_n in range(n):
                result = max(result, self.dfs(index_m, index_n, grid))

        return result

    def dfs(self, index_m, index_n, grid) -> int:
        current = grid[index_m][index_n]
        amount_gold = 0
        if current == 0:
            return amount_gold
        grid[index_m][index_n] = 0

        for offset_m, offset_n in [(0, 1), (0, -1), (1, 0), (-1, 0)]:
            index_m_next = index_m + offset_m
            index_n_next = index_n + offset_n
            if 0 <= index_m_next < len(grid) and 0 <= index_n_next < len(grid[0]):
                amount_gold = max(amount_gold, self.dfs(index_m_next, index_n_next, grid))

        grid[index_m][index_n] = current
        return current + amount_gold
```
