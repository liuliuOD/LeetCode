![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1462. [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv)

### Solution :

Method 1 (DFS + Pruning + Union Find) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.items = list(range(n))

    def find(self, value: int) -> int:
        if self.items[value] != value:
            self.items[value] = self.find(self.items[value])
        return self.items[value]

    def union(self, a: int, b: int):
        parent_a = self.find(a)
        parent_b = self.find(b)
        if parent_a != parent_b:
            self.items[parent_a] = parent_b

class Solution:
    def checkIfPrerequisite(self, num_courses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        union_find = UnionFind(num_courses)
        graph = defaultdict(list)
        for previous, current in prerequisites:
            union_find.union(previous, current)
            graph[previous].append(current)

        result = []
        for previous, current in queries:
            if union_find.find(previous) != union_find.find(current):
                result.append(False)
                continue

            visited = set()
            result.append(self.dfs(previous, visited, current, graph))

        return result

    def dfs(self, index: int, visited: Set[int], target: int, graph: Dict[int, List[int]]) -> bool:
        if index in visited:
            return False
        visited.add(index)

        if index == target:
            return True

        result = False
        for index_next in graph[index]:
            result |= self.dfs(index_next, visited, target, graph)
            if result:
                break

        return result
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def checkIfPrerequisite(self, num_courses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        graph = defaultdict(list)
        for previous, current in prerequisites:
            graph[previous].append(current)

        memoization = {}
        result = []
        for start, target in queries:
            result.append(self.dfs(start, memoization, target, graph))

        return result

    def dfs(self, index: int, memoization: Dict[Tuple[int], int], target: int, graph: Dict[int, List[int]]) -> bool:
        key = (index, target)
        if key in memoization:
            return memoization[key]

        if index == target:
            return True

        result = False
        for index_next in graph[index]:
            result |= self.dfs(index_next, memoization, target, graph)
            if result:
                break

        memoization[key] = result
        return result
```

Method 3 (DFS + Memoization + Union Find) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.items = list(range(n))

    def find(self, value: int) -> int:
        if self.items[value] != value:
            self.items[value] = self.find(self.items[value])
        return self.items[value]

    def union(self, a: int, b: int):
        parent_a = self.find(a)
        parent_b = self.find(b)
        if parent_a != parent_b:
            self.items[parent_a] = parent_b

class Solution:
    def checkIfPrerequisite(self, num_courses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        union_find = UnionFind(num_courses)
        graph = defaultdict(list)
        for previous, current in prerequisites:
            union_find.union(previous, current)
            graph[previous].append(current)

        memoization = {}
        result = []
        for start, target in queries:
            if union_find.find(start) != union_find.find(target):
                result.append(False)
                continue

            result.append(self.dfs(start, memoization, target, graph))

        return result

    def dfs(self, index: int, memoization: Dict[Tuple[int], int], target: int, graph: Dict[int, List[int]]) -> bool:
        key = (index, target)
        if key in memoization:
            return memoization[key]

        if index == target:
            return True

        result = False
        for index_next in graph[index]:
            result |= self.dfs(index_next, memoization, target, graph)
            if result:
                break

        memoization[key] = result
        return result
```

Method 4 (Topological Sort) :
```python
class Solution:
    def checkIfPrerequisite(self, num_courses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        ingress = [0] * num_courses
        graph = defaultdict(list)
        for previous, current in prerequisites:
            graph[previous].append(current)
            ingress[current] += 1

        answers = defaultdict(bool)
        queue = deque([index for index in range(num_courses) if ingress[index] == 0])
        while queue:
            current = queue.popleft()
            for index_next in graph[current]:
                answers[(current, index_next)] = True
                for index_previous in range(num_courses):
                    if answers[(index_previous, current)]:
                        answers[(index_previous, index_next)] = True

                ingress[index_next] -= 1
                if ingress[index_next] == 0:
                    queue.append(index_next)

        return [answers[(start, end)] for start, end in queries]
```

Method 5 (Floyd Warshall) :
```python
class Solution:
    def checkIfPrerequisite(self, num_courses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        graph = [[False]*num_courses for _ in range(num_courses)]
        for previous, current in prerequisites:
            graph[previous][current] = True

        for index_k in range(num_courses):
            for index_i in range(num_courses):
                for index_j in range(num_courses):
                    graph[index_i][index_j] = graph[index_i][index_j] or (graph[index_i][index_k] and graph[index_k][index_j])

        return [graph[start][end] for start, end in queries]
```
