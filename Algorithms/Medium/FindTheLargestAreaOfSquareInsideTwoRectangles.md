![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3047. [Find The Largest Area Of Square Inside Two Rectangles](https://leetcode.com/problems/find-the-largest-area-of-square-inside-two-rectangles)

### Solution :

Method 1 (In weekly contest 386, Brute Force) :
```python
class Solution:
    def largestSquareArea(self, bottomLeft: List[List[int]], topRight: List[List[int]]) -> int:
        n = len(bottomLeft)
        result = 0
        for index in range(n):
            x_start, y_start = bottomLeft[index]
            x_end, y_end = topRight[index]
            for index_next in range(n):
                if index == index_next:
                    continue

                x_next_start, y_next_start = bottomLeft[index_next]
                x_next_end, y_next_end = topRight[index_next]
                if x_next_start <= x_start <= x_next_end and y_next_start <= y_start <= y_next_end and x_next_start <= x_end <= x_next_end and y_next_start <= y_end <= y_next_end:
                    result = max(result, min(x_end-x_start, y_end-y_start)**2)
                elif x_start <= x_next_start <= x_end and y_start <= y_next_start <= y_end and x_next_end <= x_end and y_next_end <= y_end:
                    result = max(result, min(x_next_end-x_next_start, y_next_end-y_next_start)**2)
                elif y_next_start <= y_start <= y_next_end and (x_next_start <= x_start <= x_next_end or x_next_start <= x_end <= x_next_end or (x_start < x_next_start and x_end > x_next_end)):
                    result = max(result, min(y_next_end-y_start, y_end-y_start, y_next_end-y_next_start, min(x_end, x_next_end)-max(x_start, x_next_start))**2)
                elif x_start <= x_next_start <= x_end and (y_start <= y_next_start <= y_end or y_start <= y_next_end <= y_end or (y_next_start < y_start and y_next_end > y_end)):
                    result = max(result, min(x_end-x_next_start, x_end-x_start, x_next_end-x_next_start, min(y_end, y_next_end)-max(y_start, y_next_start))**2)
                elif y_next_start <= y_end <= y_next_end and (x_start <= x_next_start <= x_end or x_start <= x_next_end <= x_end or (x_next_start < x_start and x_next_end > x_end)):
                    result = max(result, min(y_end-y_next_start, y_end-y_start, y_next_end-y_next_start, min(x_end, x_next_end)-max(x_start, x_next_start))**2)
                elif x_start <= x_next_end <= x_end and (y_start <= y_next_start <= y_end or y_start <= y_next_end <= y_end or (y_next_start < y_start and y_next_end > y_end)):
                    result = max(result, min(x_next_end-x_start, x_end-x_start, x_next_end-x_next_start, min(y_end, y_next_end)-max(y_start, y_next_start))**2)

        return result
```
