![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2101. [Detonate The Maximum Bombs](https://leetcode.com/problems/detonate-the-maximum-bombs)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def maximumDetonation(self, bombs: List[List[int]]) -> int:
        result = 0
        self.bombs = bombs
        self.visited = set()
        for index in range(len(bombs)):
            result = max(result, self.dfs(index))
            self.visited.clear()
        return result

    def dfs(self, index: int) -> int:
        x, y, radius = self.bombs[index]
        result = 0
        if index in self.visited:
            return result
        result += 1

        self.visited.add(index)
        for index_target in range(len(self.bombs)):
            x_target, y_target, _ = self.bombs[index_target]
            # has been visited or out of the detonate range
            if index_target in self.visited or (x - x_target)**2 + (y - y_target)**2 > radius**2:
                continue

            result += self.dfs(index_target)
        return result
```

Method 2 (Union Find) :
```python

```
