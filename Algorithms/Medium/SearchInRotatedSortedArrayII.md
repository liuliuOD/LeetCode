![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 81. [Search In Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii)

### Solution :

Method 1 (Find Pivot by Brute Force + Binary Search) :
```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        pivot = self.findPivot(nums)
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right-left) // 2
            middle_after_pivot = (middle+pivot) % len(nums)
            if target == nums[middle_after_pivot]:
                return True
            elif target > nums[middle_after_pivot]:
                left = middle + 1
            elif target < nums[middle_after_pivot]:
                right = middle - 1
        return False

    def findPivot(self, nums: List[int]) -> int:
        for index in range(len(nums)-1):
            if nums[index] <= nums[index+1]:
                continue

            return index + 1
        return 0
```

Method 2 (Binary Search) :
```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        n = len(nums)
        left = 0
        right = n - 1
        while left <= right:
            middle = left + (right-left)//2

            if nums[middle] == target:
                return True

            if nums[middle] == nums[left]:
                left += 1
                continue

            if nums[middle] > nums[left]:
                if nums[left] <= target < nums[middle]:
                    right = middle - 1
                else:
                    left = middle + 1
            elif nums[middle] < nums[left]:
                if nums[middle] < target <= nums[right]:
                    left = middle + 1
                else:
                    right = middle - 1

        return False
```
