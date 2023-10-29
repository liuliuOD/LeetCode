![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2918. [Minimum Equal Sum Of Two Arrays After Replacing Zeros](https://leetcode.com/problems/minimum-equal-sum-of-two-arrays-after-replacing-zeros)

### Solution :

Method 1 (In weekly contest 369) :
```python
class Solution:
    def minSum(self, nums1: List[int], nums2: List[int]) -> int:
        sum1 = sum2 = 0
        amount_zero1 = amount_zero2 = 0
        for num1 in nums1:
            if num1 == 0:
                amount_zero1 += 1
            else:
                sum1 += num1
        for num2 in nums2:
            if num2 == 0:
                amount_zero2 += 1
            else:
                sum2 += num2

        temp1 = sum1 + amount_zero1
        temp2 = sum2 + amount_zero2
        result = temp1
        if temp1 > temp2:
            if amount_zero2 == 0:
                return -1

            result = temp1
        elif temp1 < temp2:
            if amount_zero1 == 0:
                return -1

            result = temp2

        return result
```
