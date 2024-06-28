![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2285. [Maximum Total Importance Of Roads](https://leetcode.com/problems/maximum-total-importance-of-roads)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M+N*Log(N))$ (M: number of elements in `roads`, N: value of `n`), Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        counter = [0] * n
        for a, b in roads:
            counter[a] += 1
            counter[b] += 1

        counter = sorted(enumerate(counter), key=lambda item: item[1], reverse=True)
        result = 0
        for _, amount in counter:
            result += amount * n
            n -= 1

        return result
```
