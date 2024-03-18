![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 452. [Minimum Number Of Arrows To Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points.sort()
        n = len(points)
        result = 1
        left = 0
        right = 1
        intersection = points[left]
        while left <= right and right < n:
            if points[right][0] <= intersection[1]:
                intersection[0] = max(intersection[0], points[right][0])
                intersection[1] = min(intersection[1], points[right][1])
            else:
                left = right
                intersection = points[left]
                result += 1

            right += 1

        return result
```
