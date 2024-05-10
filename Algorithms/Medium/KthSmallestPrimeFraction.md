![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 786. [K-th Smallest Prime Fraction](https://leetcode.com/problems/k-th-smallest-prime-fraction)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def kthSmallestPrimeFraction(self, arr: List[int], k: int) -> List[int]:
        n = len(arr)
        fractions = [(arr[i] / arr[j], arr[i], arr[j]) for i in range(n) for j in range(i+1, n)]
        fractions.sort(key=lambda item: item[0])
        return list(fractions[k-1][1:])
```

Method 2 (Binary Heap, Time Complexity: $O(N^2)$, Space Complexity: $O(K)$) :
```python
class Solution:
    def kthSmallestPrimeFraction(self, arr: List[int], k: int) -> List[int]:
        n = len(arr)
        heap = []
        for i in range(n):
            for j in range(i+1, n):
                heapq.heappush(heap, (-arr[i] / arr[j], arr[i], arr[j]))
                while len(heap) > k:
                    heapq.heappop(heap)

        return list(heapq.heappop(heap)[1:])
```
