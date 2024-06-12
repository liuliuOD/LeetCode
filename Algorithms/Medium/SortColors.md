![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 75. [Sort Colors](https://leetcode.com/problems/sort-colors)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        index_current = 0
        for color in range(3):
            for index in range(n):
                if nums[index] == color:
                    nums[index_current], nums[index] = nums[index], nums[index_current]
                    index_current += 1

            if index_current >= n:
                break
```

Method 2 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
BASE = 3

class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        colors = [0] * BASE
        for num in nums:
            colors[num] += 1

        prefix_sum = 0
        for index in range(BASE):
            while colors[index]:
                nums[prefix_sum] = index
                prefix_sum += 1
                colors[index] -= 1
```
