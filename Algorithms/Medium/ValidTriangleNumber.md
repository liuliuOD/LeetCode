![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 611. [Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        n = len(nums)
        nums.sort()
        result = 0
        for index_first in range(n):
            for index_second in range(index_first+1, n):
                for index_last in range(index_second+1, n):
                    if nums[index_first]+nums[index_second] <= nums[index_last]:
                        break

                    result += 1

        return result
```

Method 2 (Binary Search, Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        n = len(nums)
        nums.sort()
        result = 0
        for index_first in range(n):
            if nums[index_first] == 0:
                continue

            for index_second in range(index_first+1, n):
                summarization = nums[index_first] + nums[index_second]
                left = index_second + 1
                right = n
                while left < right:
                    middle = left + (right - left) // 2
                    if nums[middle] >= summarization:
                        right = middle
                    else:
                        left = middle + 1

                result += left - index_second - 1

        return result
```

Method 3 (Binary Search + Optimization, Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        n = len(nums)
        nums.sort()
        result = 0
        for index_first in range(n):
            if nums[index_first] == 0:
                continue

            left = index_first + 2
            for index_second in range(index_first+1, n):
                summarization = nums[index_first] + nums[index_second]
                right = n
                while left < right:
                    middle = left + (right - left) // 2
                    if nums[middle] >= summarization:
                        right = middle
                    else:
                        left = middle + 1

                result += left - index_second - 1

        return result
```

Method 4 (Linear Scan, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        n = len(nums)
        nums.sort()
        result = 0
        for index_first in range(n-2):
            if nums[index_first] == 0:
                continue

            index_third = index_first + 2
            for index_second in range(index_first+1, n-1):
                summarization = nums[index_first] + nums[index_second]
                while index_third < n and summarization > nums[index_third]:
                    index_third += 1

                result += index_third - index_second - 1

        return result
```
