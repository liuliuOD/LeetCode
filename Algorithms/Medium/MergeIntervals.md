![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 56. [Merge Intervals](https://leetcode.com/problems/merge-intervals)

### Solution :

Method 1 (Sort) :
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        n = len(intervals)
        result = []
        left, right = intervals[0]
        for index in range(1, n):
            left_current, right_current = intervals[index]
            if left_current == left or left_current <= right:
                right = max(right, right_current)
            else:
                result.append([left, right])
                left = left_current
                right = right_current

        result.append([left, right])
        return result
```

Method 2 (Binary Heap) :
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        heapq.heapify(intervals)
        n = len(intervals)
        result = []
        left, right = heapq.heappop(intervals)
        while intervals:
            left_current, right_current = heapq.heappop(intervals)
            if left_current == left or left_current <= right:
                right = max(right, right_current)
            else:
                result.append([left, right])
                left = left_current
                right = right_current

        result.append([left, right])
        return result
```
