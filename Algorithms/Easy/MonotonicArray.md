![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 896. [Monotonic Array](https://leetcode.com/problems/monotonic-array)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isMonotonic(self, nums: List[int]) -> bool:
        is_monotone_increasing = is_monotone_decreasing = True
        for index in range(1, len(nums)):
            if nums[index-1] > nums[index]:
                is_monotone_increasing = False
            if nums[index-1] < nums[index]:
                is_monotone_decreasing = False

            if not is_monotone_increasing and not is_monotone_decreasing:
                return False

        return True
```
