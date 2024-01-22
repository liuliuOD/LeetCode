![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 645. [Set Mismatch](https://leetcode.com/problems/set-mismatch)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        nums.sort()
        n = len(nums)
        exist = set(nums)
        result = [0, list(set(range(1, n+1))-set(nums))[0]]
        for index in range(n):
            if index+1 < n and nums[index] == nums[index+1]:
                result[0] = nums[index]
                return result
```
