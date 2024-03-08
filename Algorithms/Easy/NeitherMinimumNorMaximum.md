![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2733. [Neither Minimum Nor Maximum](https://leetcode.com/problems/neither-minimum-nor-maximum)

### Solution :

Method 1 (In weekly contest 349) :
```python
class Solution:
    def findNonMinOrMax(self, nums: List[int]) -> int:
        minimum = min(nums)
        maximum = max(nums)
        for n in nums:
            if n != minimum and n != maximum:
                return n
        return -1
```

Method 2 :
```python
class Solution:
    def findNonMinOrMax(self, nums: List[int]) -> int:
        if len(nums) < 3:
            return -1
        
        minimum = min(nums[0], nums[1])
        maximum = max(nums[0], nums[1])
        
        if nums[2] > maximum:
            return maximum
        elif nums[2] < minimum:
            return minimum
        return nums[2]
```
