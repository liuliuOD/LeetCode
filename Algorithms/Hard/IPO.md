![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 502. [IPO](https://leetcode.com/problems/ipo)

### Solution :

Method 1 (Hash Map + Binary Heap, Time Complexity: $O()$, Space Complexity: $O()$, ERROR: "Time Limit Exceeded", 32/35) :
```python
class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        n = len(profits)
        projects = defaultdict(list)
        for index in range(n):
            heapq.heappush(projects[capital[index]], -profits[index])

        capital = list(set(capital))
        capital.sort()
        for _ in range(k):
            key_projects = -1
            maximum = -inf

            for cost in capital:
                if cost > w:
                    break
                if -projects[cost][0] > maximum:
                    maximum = -projects[cost][0]
                    key_projects = cost

            if key_projects == -1:
                break

            heapq.heappop(projects[key_projects])
            if not projects[key_projects]:
                del projects[key_projects]
                capital.remove(key_projects)

            w += maximum

        return w
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        n = len(profits)
        projects = [(capital[index], profits[index]) for index in range(n)]
        projects.sort()
        index = 0
        heap = []
        for _ in range(k):
            while index < n and projects[index][0] <= w:
                heapq.heappush(heap, -projects[index][1])
                index += 1

            if not heap:
                break

            w += -heapq.heappop(heap)

        return w
```
