![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1646. [Get Maximum In Generated Array](https://leetcode.com/problems/get-maximum-in-generated-array)

### Solution :

Method 1 (Dynamic Programming) :
```python
class Solution:
    def getMaximumGenerated(self, n: int) -> int:
        memoization = {0: 0, 1: 1}
        if n < 2:
            return memoization[n]

        for index in range(2, n+1):
            if index % 2 == 0:
                memoization[index] = memoization[index/2]
                continue
            i = (index-1) / 2
            memoization[index] = memoization[i] + memoization[i+1]

        return max(memoization.values())
```
