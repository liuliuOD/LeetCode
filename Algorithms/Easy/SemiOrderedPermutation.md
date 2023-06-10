![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2717. [Semi-Ordered Permutation](https://leetcode.com/problems/semi-ordered-permutation)

### Solution :

Method 1 (In weekly contest 348) :
```python
class Solution:
    def semiOrderedPermutation(self, nums: List[int]) -> int:
        result = 0
        if nums[0] != 1:
            result += nums.index(1)
            nums.remove(1)
            nums.insert(0, 1)

        tail = len(nums)
        if nums[-1] != tail:
            temp = nums.index(tail)
            result += tail - temp - 1
        return result
```
