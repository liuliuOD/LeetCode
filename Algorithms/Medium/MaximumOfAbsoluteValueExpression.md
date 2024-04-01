![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1131. [Maximum Of Absolute Value Expression](https://leetcode.com/problems/maximum-of-absolute-value-expression)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded" (19/21), Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxAbsValExpr(self, arr1: List[int], arr2: List[int]) -> int:
        n = len(arr1)
        result = 0
        for i in range(n):
            for j in range(i+1, n):
                result = max(result, abs(arr1[i]-arr1[j])+abs(arr2[i]-arr2[j])+abs(i-j))

        return result
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxAbsValExpr(self, arr1: List[int], arr2: List[int]) -> int:
        n = len(arr1)
        result = 0
        for symbol_1, symbol_2 in [(1, 1), (1, -1), (-1, 1), (-1, -1)]:
            # Option 1
            absolute_list = []
            for index in range(n):
                absolute_list.append(symbol_1 * arr1[index] + symbol_2 * arr2[index] + index)
            """
            Option 2

            absolute_list = [symbol_1 * arr1[index] + symbol_2 * arr2[index] + index for index in range(n)]
            """

            result = max(result, max(absolute_list)-min(absolute_list))

        return result
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxAbsValExpr(self, arr1: List[int], arr2: List[int]) -> int:
        n = len(arr1)
        result = 0
        for symbol_1, symbol_2 in [(1, 1), (1, -1), (-1, 1), (-1, -1)]:
            smallest = symbol_1 * arr1[0] + symbol_2 * arr2[0] + 0
            for index in range(1, n):
                current = symbol_1 * arr1[index] + symbol_2 * arr2[index] + index
                result = max(result, current - smallest)
                smallest = min(smallest, current)

        return result
```
