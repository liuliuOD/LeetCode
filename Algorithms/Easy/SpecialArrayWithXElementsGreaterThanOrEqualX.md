![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1608. [Special Array With X Elements Greater Than Or Equal X](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def specialArray(self, nums: List[int]) -> int:
        maximum = len(nums)
        result = -1
        for candidate in range(1, maximum+1):
            amount = 0
            for num in nums:
                if num >= candidate:
                    amount += 1

            if amount == candidate:
                result = candidate
            elif amount < candidate:
                break

        return result
```
