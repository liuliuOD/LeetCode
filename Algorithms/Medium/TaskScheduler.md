![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 621. [Task Scheduler](https://leetcode.com/problems/task-scheduler)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        counter = Counter(tasks)
        queue = [-v for v in counter.values()]
        heapq.heapify(queue)
        result = 0
        while queue:
            temp_n = n + 1
            temp_tasks = []
            while temp_n and queue:
                temp_n -= 1
                temp_tasks.append(heapq.heappop(queue)+1)

            for t in temp_tasks:
                if t < 0:
                    heapq.heappush(queue, t)

            result += n + 1 if queue else n - temp_n + 1

        return result
```
