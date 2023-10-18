![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 207. [Course Schedule](https://leetcode.com/problems/course-schedule)

### Solution :

Method 1 (DFS, Time Complexity: $O(V+E)$) :
```python
from enum import Enum
class Color(Enum):
    VISITED = 1
    UNVISITED = 2
    FINISH = 3

class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        draw_colors = [Color.UNVISITED for _ in range(num_courses)]
        graph = set()
        for course_target, course_need in prerequisites:
            graph.add(self.graphKey(course_target, course_need))

        for index in range(num_courses):
            if self.hasCycle(index, graph, draw_colors, num_courses):
                return False

        return True

    def hasCycle(self, index: int, graph: Set[str], draw_colors: List[Color], num_courses: int) -> bool:
        if draw_colors[index] == Color.VISITED:
            return True
        draw_colors[index] = Color.VISITED

        for index_need in range(num_courses):
            if self.graphKey(index, index_need) not in graph or draw_colors[index_need] == Color.FINISH:
                continue

            if draw_colors[index_need] == Color.VISITED or (draw_colors[index_need] == Color.UNVISITED and self.hasCycle(index_need, graph, draw_colors, num_courses)):
                return True

        draw_colors[index] = Color.FINISH
        return False

    def graphKey(self, target: int, need: int) -> str:
        return f'{target}-{need}'
```

Method 2 (BFS + Topological Sort (Kahn's Algorithm)) :
```python
class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        incoming_edges = [0 for _ in range(num_courses)]
        adjustment_list = [[] for _ in range(num_courses)]
        for course_target, course_need in prerequisites:
            incoming_edges[course_need] += 1
            adjustment_list[course_target].append(course_need)

        queue = deque()
        for index_node, edges in enumerate(incoming_edges):
            if edges == 0:
                queue.append(index_node)

        amount_acyclic = 0
        while queue:
            index = queue.popleft()

            amount_acyclic += 1
            for index_next in adjustment_list[index]:
                incoming_edges[index_next] -= 1
                if incoming_edges[index_next] == 0:
                    queue.append(index_next)

        return amount_acyclic == num_courses
```
