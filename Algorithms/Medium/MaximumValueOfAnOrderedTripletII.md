![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2874. [Maximum Value Of An Ordered Triplet II](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
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

Method 2 (Prefix & Suffix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumTripletValue(self, nums: List[int]) -> int:
        n = len(nums)
        maximumLeft = [float('-inf')] * (n+1)
        for index, num in enumerate(nums):
            maximumLeft[index+1] = max(num, maximumLeft[index])

        maximumRight = [float('-inf')] * (n+1)
        for index in reversed(range(n)):
            maximumRight[index] = max(nums[index], maximumRight[index+1])

        result = float('-inf')
        for index in range(1, n-1):
            result = max(result, (maximumLeft[index]-nums[index])*maximumRight[index+1])

        return result if result > 0 else 0
```

Method 3 (Loop, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maximumTripletValue(self, nums: List[int]) -> int:
        result = maximum_minus = maximum_num = 0
        for num in nums:
            result = max(result, maximum_minus * num)
            maximum_minus = max(maximum_minus, maximum_num - num)
            maximum_num = max(maximum_num, num)

        return result
```
