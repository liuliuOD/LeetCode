![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1971. [Find If Path Exists In Graph](https://leetcode.com/problems/find-if-path-exists-in-graph)

### Solution :

Method 1 :
```rust
```

### Solution :

Method 1 (DFS, Time Complexity: $O(V+E)$ (V: amount of vertices = `n`, E: amount of linked edges = `edges`), Space Complexity: $O(V+E)$) :
```python
class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        graph = [[] for _ in range(n)]
        for u, v in edges:
            graph[u].append(v)
            graph[v].append(u)

        visited = set([source])
        self.result = False
        self.traverse(source, visited, destination, graph)
        return self.result

    def traverse(self, source: int, visited: Set[int], destination: int, graph: List[List[int]]):
        if source == destination:
            self.result = True
            return
        visited.add(source)

        for move in graph[source]:
            if move in visited:
                continue

            self.traverse(move, visited, destination, graph)
            if self.result:
                break
```

Method 2 (Union Find, Time Complexity: $O(V+E)$ (V: amount of vertices = `n`, E: amount of linked edges = `edges`), Space Complexity: $O(V+E)$) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.items = list(range(n))

    def find(self, target: int) -> int:
        if self.items[target] != target:
            target = self.find(self.items[target])

        return target

    def union(self, a: int, b: int) -> None:
        root_a, root_b = self.find(a), self.find(b)
        if root_a != root_b:
            self.items[root_a] = root_b

class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        uf = UnionFind(n)
        for u, v in edges:
            uf.union(u, v)

        return uf.find(source) == uf.find(destination)
```
