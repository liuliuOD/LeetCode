![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1615. [Maximal Network Rank](https://leetcode.com/problems/maximal-network-rank)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def maximalNetworkRank(self, n: int, roads: List[List[int]]) -> int:
        result = [0] * n
        connected = set()

        for road in roads:
            result[road[0]] += 1
            result[road[1]] += 1
            connected.add((road[0], road[1]))
            connected.add((road[1], road[0]))

        maximum = 0
        for index_left in range(n):
            for index_right in range(index_left+1, n):
                maximum = max(maximum, result[index_left] + result[index_right] + (-1 if (index_left, index_right) in connected else 0))

        return maximum
```

Method2 (Brute Force + Prune) :
```python
class Solution:
    def maximalNetworkRank(self, n: int, roads: List[List[int]]) -> int:
        result = [0] * n
        connected = set()

        for road in roads:
            result[road[0]] += 1
            result[road[1]] += 1
            connected.add((road[0], road[1]))
            connected.add((road[1], road[0]))

        result = sorted([(value, key) for key, value in enumerate(result)], reverse=True)

        maximum = 0
        for index_left in range(n):
            for index_right in range(index_left+1, n):
                current = result[index_left][0] + result[index_right][0] + (-1 if (result[index_left][1], result[index_right][1]) in connected else 0)
                if maximum-current > 2:
                    return maximum

                maximum = max(maximum, current)

        return maximum
```
