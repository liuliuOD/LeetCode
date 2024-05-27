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

Method 2 (Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def specialArray(self, nums: List[int]) -> int:
        nums.sort()
        n = len(nums)

        for candidate in range(1, nums[-1]+1):
            left, right = 0, n - 1
            while left <= right:
                middle = left + (right - left)//2
                if nums[middle] >= candidate:
                    right = middle - 1
                else:
                    left = middle + 1

            if n - left == candidate:
                return candidate

        return -1
```
