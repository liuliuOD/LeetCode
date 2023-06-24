![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2740. [Find The Value Of The Partition](https://leetcode.com/problems/find-the-value-of-the-partition)

### Solution :

Method 1 (In weekly contest 350) :
```python
class Solution:
    def findValueOfPartition(self, nums: List[int]) -> int:
        nums.sort()
        
        result = 10**9
        for index in range(len(nums)-1):
            result = min(result, nums[index+1] - nums[index])
        return result
```
