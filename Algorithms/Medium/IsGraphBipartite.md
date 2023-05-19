![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 785. [Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        self.colored = [0] * n
        for i in range(0, n):
            if self.colored[i] == 0:
                if not self.dfs(i, graph, 1):
                    return False
        return True
    
    def dfs(self, i: int, graph: List[List[int]], color: int) -> bool:
        if self.colored[i] != 0:
            return self.colored[i] == color
        
        self.colored[i] = color
        for j in graph[i]:
            if not self.dfs(j, graph, -color):
                return False
        return True
```
