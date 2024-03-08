![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 209. [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum)

### Solution :

Method 1 (Two Pointer, Time Complexity: O(N)) :
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        result = float('inf')
        n = len(nums)
        pointer_left = 0
        pointer_right = 0
        temp = 0
        while pointer_left <= pointer_right and pointer_right < n:
            temp += nums[pointer_right]

            while temp >= target:
                result = min(result, pointer_right - pointer_left + 1)
                temp -= nums[pointer_left]
                pointer_left += 1

            pointer_right += 1
        
        return result if result != float('inf') else 0
```
