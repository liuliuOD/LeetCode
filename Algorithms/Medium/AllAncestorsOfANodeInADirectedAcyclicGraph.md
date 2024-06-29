![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2192. [All Ancestors Of A Node In A Directed Acyclic Graph](https://leetcode.com/problems/all-ancestors-of-a-node-in-a-directed-acyclic-graph)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 37/80) :
```python
class Solution:
    def getAncestors(self, n: int, edges: List[List[int]]) -> List[List[int]]:
        graph_to = [[] for _ in range(n)]
        graph_from = [[] for _ in range(n)]
        for n_from, n_to in edges:
            graph_to[n_to].append(n_from)
            graph_from[n_from].append(n_to)

        queue = deque()
        for index, parents in enumerate(graph_to):
            if not parents:
                queue.append(index)

        result = [[] for _ in range(n)]
        while queue:
            index_current = queue.popleft()

            queue.extend(graph_from[index_current])
            parents: set[int] = set()
            for index_parent in graph_to[index_current]:
                parents.add(index_parent)
                parents.update(result[index_parent])

            result[index_current] = list(parents)
            result[index_current].sort()

        return result
```

Method 2 (DFS + Reverse Graph, Time Complexity: $O((M+N)*Log(N))$, Space Complexity: $O(M+N)$) :
```python
class Solution:
    def getAncestors(self, n: int, edges: List[List[int]]) -> List[List[int]]:
        outgress = [0] * n
        graph = [[] for _ in range(n)]
        for n_from, n_to in edges:
            graph[n_to].append(n_from)
            outgress[n_from] += 1

        visited: set[int] = set()
        self.result: list[list[int]] = [[] for _ in range(n)]
        for index, amount_out in enumerate(outgress):
            if amount_out > 0:
                continue

            self.dfs(index, visited, graph)

        return self.result

    def dfs(self, index: int, visited: set[int], graph: list[list[int]]) -> list[int]:
        if index in visited:
            return self.result[index]
        visited.add(index)

        parents: set[int] = set()
        for index_parent in graph[index]:
            parents.update([index_parent] + self.dfs(index_parent, visited, graph))

        parents_sorted = sorted(list(parents))
        self.result[index] = parents_sorted.copy()
        bisect.insort(parents_sorted, index)
        return parents_sorted
```
