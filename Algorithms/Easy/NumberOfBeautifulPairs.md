![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2748. [Number Of Beautiful Pairs](https://leetcode.com/problems/number-of-beautiful-pairs)

### Solution :

Method 1 (In weekly contest 351) :
```python
import math
class Solution:
    def countBeautifulPairs(self, nums: List[int]) -> int:
        result = 0
        for i in range(len(nums)):
            first = nums[i]
            while first >= 10:
                first = first // 10
            for j in range(i+1, len(nums)):
                second = nums[j] % 10
                if math.gcd(first, second) == 1:
                    result += 1
        return result
```
