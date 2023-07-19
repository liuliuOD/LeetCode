![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2779. [Maximum Beauty Of An Array After Applying Operation](https://leetcode.com/problems/maximum-beauty-of-an-array-after-applying-operation)

### Solution :

Method 1 (Two Pointer) :
```python
class Solution:
    def maximumBeauty(self, nums: List[int], k: int) -> int:
        n = len(nums)
        pointer_left = 0
        pointer_right = 0
        result = 0
        nums.sort()
        while pointer_left < n and pointer_right < n:
            if nums[pointer_right]-nums[pointer_left] > k*2:
                pointer_left += 1
                continue

            result = max(result, pointer_right-pointer_left+1)
            pointer_right += 1
        return result
```
