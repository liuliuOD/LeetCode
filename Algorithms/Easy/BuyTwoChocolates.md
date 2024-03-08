![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2706. [Buy Two Chocolates](https://leetcode.com/problems/buy-two-chocolates)

### Solution :

Method 1 (In biweekly contest 105, Binary Heap, Minimum Heap, Time Complexity: $(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        heapq.heapify(prices)
        cost = 0
        for _ in range(2):
            cost += heapq.heappop(prices)
        return money if cost > money else money - cost
```

Method 2 (Time Complexity: $(N*Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        heap = []
        for price in prices:
            heapq.heappush(heap, -price)
            if len(heap) > 2:
                heapq.heappop(heap)

        return money if money+sum(heap) < 0 else money+sum(heap)
```

Method 3 (Time Complexity: $(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        prices.sort()

        return money if money-prices[0]-prices[1] < 0 else money-prices[0]-prices[1]
```

Method 4 (Time Complexity: $(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        minimum = inf
        minimum_2 = inf
        for price in prices:
            if price < minimum:
                minimum, minimum_2 = price, minimum
            elif price < minimum_2:
                minimum_2 = price

        return money if minimum+minimum_2 > money else money-minimum-minimum_2
```
