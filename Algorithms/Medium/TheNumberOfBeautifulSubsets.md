![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2597. [The Number Of Beautiful Subsets](https://leetcode.com/problems/the-number-of-beautiful-subsets)

### Solution :

Method 1 (Bit Mask + Brute Force, ERROR: "Time Limit Exceeded", 56 / 1307) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        n = len(nums)
        result = 0
        for bitwise in range(1, 1 << n):
            subset = []
            for index in range(n):
                if ((1 << index) & bitwise) == 0:
                    continue

                for num in subset:
                    if abs(num - nums[index]) == k:
                        break
                else:
                    subset.append(nums[index])
                    continue

                break
            else:
                result += 1
        return result
```
