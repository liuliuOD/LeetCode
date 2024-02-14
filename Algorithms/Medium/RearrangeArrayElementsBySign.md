![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2149. [Rearrange Array Elements By Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        positive = []
        negative = []
        for num in nums:
            if num < 0:
                negative.append(num)
            else:
                positive.append(num)

        result = []
        while positive or negative:
            if positive:
                result.append(positive.pop(0))
            if negative:
                result.append(negative.pop(0))

        return result
```
