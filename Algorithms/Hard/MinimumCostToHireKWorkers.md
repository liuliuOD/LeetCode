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
