![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2706. [Buy Two Chocolates](https://leetcode.com/problems/buy-two-chocolates)

### Solution :

Method 1 (In biweekly contest 105, Minimum Heap) :
```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        heapq.heapify(prices)
        cost = 0
        for _ in range(2):
            cost += heapq.heappop(prices)
        return money if cost > money else money - cost
```
