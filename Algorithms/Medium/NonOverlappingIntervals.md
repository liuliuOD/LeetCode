![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 435. [Non Overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals)

### Solution :

Method 1 (Heap) :
```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        heap = intervals
        heapq.heapify(heap)
        end_previous = heapq.heappop(heap)[1]

        result = 0
        while heap:
            start_current, end_current = heapq.heappop(heap)
            if end_previous > start_current:
                result += 1
                end_previous = min(end_previous, end_current)
            else:
                end_previous = end_current

        return result
```

Method 2 (Greedy) :
```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key=lambda item: item[0])
        end_previous = intervals[0][1]
        result = 0
        for index in range(1, len(intervals)):
            start_current, end_current = intervals[index]
            if end_previous <= start_current:
                end_previous = end_current
            else:
                end_previous = min(end_previous, end_current)
                result += 1
        
        return result
```
