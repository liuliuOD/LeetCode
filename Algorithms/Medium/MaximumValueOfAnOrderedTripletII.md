![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2874. [Maximum Value Of An Ordered Triplet II](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$) :
```python
class Solution:
    def maximumTripletValue(self, nums: List[int]) -> int:
        result = 0
        stack = []
        i_minus_j = 0
        for num in nums:
            result = max(result, i_minus_j * num)

            while stack and stack[-1] <= num:
                stack.pop()

            i_minus_j = max(i_minus_j, (stack[0] - num) if stack else 0)

            stack.append(num)

        return result
```
