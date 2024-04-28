![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 834. [Sum Of Distances In Tree](https://leetcode.com/problems/sum-of-distances-in-tree)

### Solution :

Method 1 (BFS, ERROR: "Time Limit Exceeded", 64/74, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sumOfDistancesInTree(self, n: int, edges: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(n)]
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)

        result = [0] * n
        for index in range(n):
            result[index] = self.traverse(index, graph)

        return result

    def traverse(self, index: int, graph: List[List[int]]) -> int:
        visited: Set[int] = set([index])
        result = 0
        depth = 0
        queue = deque(graph[index])
        while queue:
            depth += 1
            amount = len(queue)
            for _ in range(amount):
                index_current = queue.popleft()
                if index_current in visited:
                    continue
                visited.add(index_current)
                result += depth

                for index_next in graph[index_current]:
                    if index_next in visited:
                        continue

                    queue.append(index_next)

        return result
```

Method 2 (Reroot DFS + BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sumOfDistancesInTree(self, n: int, edges: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(n)]
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)

        sub_nodes = [1] * n
        self.traverse(0, None, sub_nodes, graph)

        result = [0] * n
        result[0] = self.getDistances(0, graph)
        self.reroot(0, None, result, sub_nodes, graph)
        return result

    def getDistances(self, index: int, graph: List[List[int]]) -> int:
        visited: Set[int] = set([index])
        result = 0
        depth = 0
        queue = deque(graph[index])
        while queue:
            depth += 1
            amount = len(queue)
            for _ in range(amount):
                index_current = queue.popleft()
                if index_current in visited:
                    continue
                visited.add(index_current)
                result += depth

                for index_next in graph[index_current]:
                    if index_next in visited:
                        continue

                    queue.append(index_next)

        return result

    def traverse(self, index: int, index_previous: int | None, sub_nodes: List[int], graph: List[List[int]]):
        amount_children = 0
        for index_next in graph[index]:
            if index_next == index_previous:
                continue

            self.traverse(index_next, index, sub_nodes, graph)
            sub_nodes[index] += sub_nodes[index_next]

    def reroot(self, index: int, index_previous: int | None, result: List[int], sub_nodes: List[int], graph: List[List[int]]):
        for index_next in graph[index]:
            if index_next == index_previous:
                continue

            """
            # Option 1

            result[index_next] = result[index] - sub_nodes[index_next] + (len(result) - sub_nodes[index_next])
            """
            # Option 2
            result[index_next] = result[index] + len(result) - 2 * sub_nodes[index_next]

            self.reroot(index_next, index, result, sub_nodes, graph)
```
