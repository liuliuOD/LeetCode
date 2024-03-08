![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2750. [Ways To Split Array Into Good Subarrays](https://leetcode.com/problems/ways-to-split-array-into-good-subarrays)

### Solution :

Method 1 (In weekly contest 351) :
```python
MOD = 10**9 + 7
class Solution:
    def numberOfGoodSubarraySplits(self, nums: List[int]) -> int:
        position_one = []
        for index in range(len(nums)):
            if nums[index] != 1:
                continue
            position_one.append(index)

        if len(position_one) < 2:
            return len(position_one)
        elif len(position_one) >= 2:
            result = 1
            for index in range(1, len(position_one)):
                result = (result * (position_one[index] - position_one[index-1])) % MOD
            return result
```
