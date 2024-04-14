![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 85. [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        m, n =len(matrix), len(matrix[0])
        heights = [0] * (n+1)
        result: int = 0
        for row in matrix:
            for index, value in enumerate(row):
                if value == '0':
                    heights[index] = 0
                elif value == '1':
                    heights[index] += 1

            stack = []
            for index, height in enumerate(heights):
                while stack and height < heights[stack[-1]]:
                    height_previous = heights[stack.pop()]
                    width = index - stack[-1] - 1 if stack else index
                    result = max(result, height_previous * width)

                stack.append(index)

        return result
```
