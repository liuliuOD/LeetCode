![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 268. [Missing Number](https://leetcode.com/problems/missing-number)

### Solution :

Method 1 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        result = 0
        for item in sorted(nums):
            if item != result:
                return result
            result += 1
        return result
```

Method 2 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        nums.sort()
        for index, num in enumerate(nums):
            if index != num:
                return index

        return len(nums)
```

Method 3 (Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        nums.sort()
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] == middle:
                left = middle + 1
            else:
                right = middle - 1
        return left
```
