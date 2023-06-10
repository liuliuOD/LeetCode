![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1802. [Maximum Value At A Given Index In A Bounded Array](https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def maxValue(self, n: int, index: int, maxSum: int) -> int:
        self.n = n
        self.index = index
        left = 1
        right = 10**9
        while left <= right:
            middle = left + (right - left) // 2
            if self.minimumSum(middle-1) > maxSum - n:
                right = middle - 1
            else:
                left = middle + 1
        return right
        
    def minimumSum(self, value) -> int:
        value_subset_left = max(0, value - self.index)
        subset_left_sum = (value + value_subset_left) * (value - value_subset_left + 1) // 2
        value_subset_right = max(0, value - (self.n - self.index - 1))
        subset_right_sum = (value + value_subset_right) * (value - value_subset_right + 1) // 2
        return subset_left_sum + subset_right_sum - value
```
