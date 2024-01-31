![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 739. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        monotonic_stack = []
        result = [0] * n
        for index in range(n):
            while monotonic_stack and temperatures[monotonic_stack[-1]] < temperatures[index]:
                index_result = monotonic_stack.pop()
                result[index_result] = index - index_result

            monotonic_stack.append(index)

        return result
```
