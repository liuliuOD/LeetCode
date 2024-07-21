![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2392. [Build A Matrix With Conditions](https://leetcode.com/problems/build-a-matrix-with-conditions)

### Solution :

Method 1 (Topological Sort + Kahn's Algorithm, Time Complexity: $O(MAX(K^2, M+N))$, Space Complexity: $O(MAX(K^2, M+N))$ (M: numbers of the elements in `row_conditions`, N: numbers of the elements in `col_conditions`, K: the value of `k`)) :
```python
class Solution:
    def buildMatrix(self, k: int, row_conditions: List[List[int]], col_conditions: List[List[int]]) -> List[List[int]]:
        ordered_row: list[int] = self.kahns_algorithm(row_conditions, k)
        ordered_col: list[int] = self.kahns_algorithm(col_conditions, k)
        if not ordered_row or not ordered_col:
            return []

        result = [[0]*k for _ in range(k)]
        for index_m in range(k):
            for index_n in range(k):
                if ordered_row[index_m] == ordered_col[index_n]:
                    result[index_m][index_n] = ordered_row[index_m]

        return result

    def kahns_algorithm(self, conditions: list[list[int]], n: int) -> list[int]:
        graph = [[] for _ in range(n+1)]
        ingress = [0] * (n + 1)
        for indegree, outdegree in conditions:
            graph[indegree].append(outdegree)
            ingress[outdegree] += 1

        queue = deque()
        for index in range(1, n+1):
            if ingress[index] == 0:
                queue.append(index)

        result: list[int] = []
        while queue:
            index = queue.popleft()
            result.append(index)
            for outdegree in graph[index]:
                ingress[outdegree] -= 1
                if ingress[outdegree] == 0:
                    queue.append(outdegree)

        return result if len(result) == n else []
```
