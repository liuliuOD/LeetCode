![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1791. [Find Center Of Star Graph](https://leetcode.com/problems/find-center-of-star-graph)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findCenter(self, edges: List[List[int]]) -> int:
        point_1, point_2, point_3 = None, None, None

        for u, v in edges:
            if u in [point_1, point_2, point_3]:
                return u
            if v in [point_1, point_2, point_3]:
                return v

            if point_1 is None:
                point_1 = u
            elif point_2 is None:
                point_2 = u
            elif point_3 is None:
                point_3 = u
            else:
                point_1 = u
            if point_1 is None:
                point_1 = v
            elif point_2 is None:
                point_2 = v
            elif point_3 is None:
                point_3 = v
            else:
                point_2 = v

        return -1
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findCenter(self, edges: List[List[int]]) -> int:
        for index in range(1, len(edges)):
            if edges[index-1][0] in edges[index]:
                return edges[index-1][0]
            elif edges[index-1][1] in edges[index]:
                return edges[index-1][1]

        return -1
```
