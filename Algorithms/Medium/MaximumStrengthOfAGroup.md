![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2708. [Maximum Strength Of A Group](https://leetcode.com/problems/maximum-strength-of-a-group)

### Solution :

Method 1 (In biweekly contest 105) :
```python
class Solution:
    def maxStrength(self, nums: List[int]) -> int:
        neg = []
        pos = []
        zero = []
        result = 1
        for num in nums:
            if num < 0:
                neg.append(num)
            elif num > 0:
                pos.append(num)
                result *= num
            else:
                zero.append(num)

        if result == 1 and len(zero) == 0 and len(pos) == 0 and len(neg) == 1:
            result = neg.pop()
        elif len(pos) == 0 and len(neg) < 2 and len(zero) > 0:
            result = 0
        else:
            heapq.heapify(neg)
            for _ in range(len(neg) // 2 * 2):
                result *= heapq.heappop(neg)
        return result
```
