![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 857. [Minimum Cost To Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 41/46, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
        n = len(quality)
        fraction = [(wage[index] / quality[index], index) for index in range(n)]

        result = inf
        fraction.sort()
        for index in range(k-1, n):
            current = fraction[index]
            cost = current[0]
            candidates = [cost * quality[current[1]]]
            for index_previous in range(index):
                previous = fraction[index_previous]
                candidates.append(cost * quality[previous[1]])
            candidates.sort()
            result = min(result, sum(candidates[:k]))

        return result
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N+K)$) :
```python
class Solution:
    def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
        n = len(quality)
        fraction = [(wage[index] / quality[index], index) for index in range(n)]
        fraction.sort()

        result = inf
        heap = []
        choose_quality_sum = 0
        for index in range(n):
            current = fraction[index]
            cost = current[0]
            current_quality = quality[current[1]]
            choose_quality_sum += current_quality
            heapq.heappush(heap, -current_quality)
            if len(heap) > k:
                choose_quality_sum += heapq.heappop(heap)
            if len(heap) == k:
                result = min(result, cost * choose_quality_sum)

        return result
```
