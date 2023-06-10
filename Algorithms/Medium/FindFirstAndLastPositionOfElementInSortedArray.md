![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 34. [Find First And Last Position Of Element In Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        start = -1
        end = -1
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] < target:
                left = middle + 1
            else:
                right = middle - 1
        if left < len(nums) and nums[left] == target:
            start = left
        
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] <= target:
                left = middle + 1
            else:
                right = middle - 1
        if right >= 0 and nums[right] == target:
            end = right
        
        return [start, end]
```
