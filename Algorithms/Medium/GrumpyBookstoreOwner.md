![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1052. [Grumpy Bookstore Owner](https://leetcode.com/problems/grumpy-bookstore-owner)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(N)$ (N: length of `customers`), Space Complexity: $O(1)$) :
```python
class Solution:
    def maxSatisfied(self, customers: List[int], grumpy: List[int], minutes: int) -> int:
        cumulative = 0
        maximum = 0
        result = 0
        for index in range(len(customers)):
            if grumpy[index] == 1:
                cumulative += customers[index]
            else:
                result += customers[index]

            if index >= minutes and grumpy[index-minutes] == 1:
                cumulative -= customers[index-minutes]

            maximum = max(maximum, cumulative)

        return result + maximum
```
