![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 815. [Bus Routes](https://leetcode.com/problems/bus-routes)

### Solution :

Method 1 (BFS) :
```python
class Solution:
    def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
        if source == target:
            return 0

        # find connection between each station
        mapping = defaultdict(list)
        for index, stations in enumerate(routes):
            for station in stations:
                mapping[station].append(index)

        queue = deque(mapping[source])
        visited = set(mapping[source])
        result = 1
        while queue:
            amount = len(queue)

            for _ in range(amount):
                current = queue.popleft()
                for station_next in routes[current]:
                    if station_next == target:
                        return result

                    for index_next in mapping[station_next]:
                        if index_next in visited:
                            continue
                        visited.add(index_next)

                        queue.append(index_next)

            result += 1

        return -1
```

Method 2 (BFS) :
```python
class Solution:
    def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
        if source == target:
            return 0

        # find connection between each route
        n = len(routes)
        routes_set = [set(group) for group in routes]
        graph = [[] for _ in range(n)]
        for index in range(n):
            for index_next in range(index+1, n):
                if any([key for key, amount in Counter(list(routes_set[index])+list(routes_set[index_next])).items() if amount > 1]):
                    graph[index].append(index_next)
                    graph[index_next].append(index)

        queue = deque()
        for index, group_set in enumerate(routes_set):
            if source in group_set:
                queue.append(index)

        visited = set()
        result = 1
        while queue:
            amount = len(queue)

            for _ in range(amount):
                current = queue.popleft()
                if target in routes_set[current]:
                    return result

                for index_next in graph[current]:
                    if index_next in visited:
                        continue
                    visited.add(index_next)

                    queue.append(index_next)

            result += 1

        return -1
```
