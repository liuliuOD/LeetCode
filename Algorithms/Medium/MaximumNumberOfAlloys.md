![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2861. [Maximum Number Of Alloys](https://leetcode.com/problems/maximum-number-of-alloys)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(K*N*Log(10^9))$ (N: value of parameter `n`, K: value of parameter `k`)) :
```python
class Solution:
    def maxNumberOfAlloys(self, n: int, k: int, budget: int, composition: List[List[int]], stock: List[int], cost: List[int]) -> int:
        """
        n: different types of metals available
        k: amount of machines
        """
        result = 0
        for index in range(k):
            left = 0
            right = 1_000_000_000
            while left <= right:
                middle = left + (right - left)//2

                if self.valid(middle, n, composition[index], budget, stock, cost):
                    left = middle + 1
                else:
                    right = middle - 1

            result = max(result, right)

        return result

    def valid(self, amount: int, n: int, composition: List[int], budget: int, stock: List[int], cost: List[int]) -> bool:
        amount_cost = 0
        for index in range(n):
            amount_cost += max(0, composition[index]*amount - stock[index]) * cost[index]

        return amount_cost <= budget
```
