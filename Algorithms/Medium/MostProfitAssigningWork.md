![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 826. [Most Profit Assigning Work](https://leetcode.com/problems/most-profit-assigning-work)

### Solution :

Method 1 (Time Complexity: $O(M*Log(M)+N*Log(N))$, Space Complexity: $O(M+N)$) :
```python
class Solution:
    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:
        works = sorted((d, p) for d, p in zip(difficulty, profit))
        result = 0
        index_works = 0
        profit_maximum = 0
        for w in sorted(worker):
            while index_works < len(works) and works[index_works][0] <= w:
                profit_maximum = max(profit_maximum, works[index_works][1])
                index_works += 1

            result += profit_maximum

        return result
```

Method 2 (Time Complexity: $O(M*Log(M)+N*Log(N))$, Space Complexity: $O(M+N)$) :
```python
class Solution:
    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:
        works = sorted([(d, p) for d, p in zip(difficulty, profit)], reverse=True)
        result = 0
        profit_maximum = 0
        for w in sorted(worker):
            while works and works[-1][0] <= w:
                profit_maximum = max(profit_maximum, works.pop()[1])

            result += profit_maximum

        return result
```
