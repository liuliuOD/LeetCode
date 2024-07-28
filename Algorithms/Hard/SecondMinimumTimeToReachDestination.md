![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2045. [Second Minimum Time To Reach Destination](https://leetcode.com/problems/second-minimum-time-to-reach-destination)

### Solution :

Method 1 (Dijkstra, Time Complexity: $O(N+E*Log(N))$, Space Complexity: $O(N+E)$ (N: the value of `n`, E: numbers of the elements in `edges`)) :
```python
class Solution:
    def secondMinimum(self, n: int, edges: List[List[int]], time: int, change: int) -> int:
        graph = [[] for _ in range(n+1)]
        for u, v in edges:
            graph[u].append(v)
            graph[v].append(u)

        distance_first, distance_second = [inf]*(n+1), [inf]*(n+1)
        frequency = [0] * (n+1)
        distance_first[1] = 0
        heap = [(0, 1)]
        while heap:
            distance, index = heapq.heappop(heap)
            
            frequency[index] += 1
            if frequency[index] > 1 and index == n:
                return distance

            if (distance // change)%2:
                distance = (distance // change + 1)*change + time
            else:
                distance += time

            for index_next in graph[index]:
                if frequency[index_next] > 1:
                    continue

                if distance_first[index_next] > distance:
                    distance_second[index_next] = distance_first[index_next]
                    distance_first[index_next] = distance
                    heapq.heappush(heap, (distance, index_next))
                elif distance_second[index_next] > distance and distance_first[index_next] != distance:
                    distance_second[index_next] = distance
                    heapq.heappush(heap, (distance, index_next))

        return 0
```
