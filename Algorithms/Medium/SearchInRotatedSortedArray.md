![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 33. [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        pivot = self.findPivotIndex(nums)
        left = 0
        right = len(nums)
        while left <= right:
            middle_ordered = left + (right - left) // 2
            middle_nums = (middle_ordered + pivot) % len(nums)
            if nums[middle_nums] == target:
                return middle_nums
            elif nums[middle_nums] > target:
                right = middle_ordered - 1
            elif nums[middle_nums] < target:
                left = middle_ordered + 1
        return -1

    def findPivotIndex(self, nums: List[int]) -> int:
        tail = nums[-1]
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] > tail:
                left = middle + 1
            else:
                right = middle - 1
        return left
```
