![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 210. [Course Schedule II](https://leetcode.com/problems/course-schedule-ii)

### Solution :

Method 1 (Topological Sort, Time Complexity: $O(M+N)$ (M: value of `num_courses`, N: length of `prerequisites`)) :
```python
class Solution:
    def findOrder(self, num_courses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = defaultdict(list)
        ingress = [0] * num_courses
        for end, start in prerequisites:
            graph[start].append(end)
            ingress[end] += 1

        result = []
        queue = deque([index for index in range(num_courses) if ingress[index] == 0])
        while queue:
            index = queue.popleft()
            if index not in result:
                result.append(index)

            for item in graph[index]:
                if item in result:
                    continue

                ingress[item] -= 1
                if ingress[item] == 0:
                    queue.append(item)

        return result if len(result) == num_courses else []
```

Method 2 (DFS, Time Complexity: $O(M+N)$) :
```python
class Solution:
    def findOrder(self, num_courses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = defaultdict(list)
        for end, start in prerequisites:
            graph[start].append(end)

        visited = [0] * num_courses
        self.result = []
        for index in range(num_courses):
            if self.dfs(index, visited, graph):
                return []

        return self.result[::-1]

    def dfs(self, index, visited, graph) -> bool:
        # has cycle
        if visited[index] == -1:
            return True
        # has been added into result
        if visited[index] == 1:
            return False
        visited[index] = -1

        for index_next in graph[index]:
            if self.dfs(index_next, visited, graph):
                return False

        self.result.append(index)
        visited[index] = 1
        return False
```

Method 3 (DFS, Time Complexity: $O(M+N)$) :
```python
from enum import Enum
class Status(Enum):
    VISITING = 1
    UNVISITED = 0
    VISITED = -1

class Solution:
    def findOrder(self, num_courses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = defaultdict(list)
        for end, start in prerequisites:
            graph[start].append(end)

        status = [Status.UNVISITED] * num_courses
        self.result = []
        for index in range(num_courses):
            if self.dfs(index, status, graph):
                return []

        return self.result[::-1]

    def dfs(self, index, status, graph) -> bool:
        # has cycle
        if status[index] == Status.VISITING:
            return True
        # has been added into result
        if status[index] == Status.VISITED:
            return False
        status[index] = Status.VISITING

        for index_next in graph[index]:
            if self.dfs(index_next, status, graph):
                return False

        self.result.append(index)
        status[index] = Status.VISITED
        return False
```
