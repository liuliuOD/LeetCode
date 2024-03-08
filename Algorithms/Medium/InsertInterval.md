![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 57. [Insert Interval](https://leetcode.com/problems/insert-interval)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def insert(self, intervals: List[List[int]], interval_new: List[int]) -> List[List[int]]:
        result = []
        for left, right in intervals:
            if left <= interval_new[0] <= right or left <= interval_new[1] <= right or (interval_new[0] < left and interval_new[1] > right):
                interval_new = [min(left, interval_new[0]), max(right, interval_new[1])]
            else:
                result.append([left, right])
        result.append(interval_new)

        return sorted(result)
```

Method 2 (Brute Force) :
```python
class Solution:
    def insert(self, intervals: List[List[int]], interval_new: List[int]) -> List[List[int]]:
        result = []
        for left, right in intervals:
            if left > interval_new[1] or right < interval_new[0]:
                result.append([left, right])
            else:
                interval_new = [min(left, interval_new[0]), max(right, interval_new[1])]
        result.append(interval_new)

        return sorted(result)
```

Method 3 (Line Sweep Algorithm) :
```python
class Solution:
    def insert(self, intervals: List[List[int]], interval_new: List[int]) -> List[List[int]]:
        START = -1
        END = 1
        heap = []
        """
        the order of interval_new need to be in the tail, that can keep order of heap.
        if swap the values of START and END, will occur error when exist overlapping in tail of i-1 and start of i, eg: [[4, 8], [8, 10]]
        """
        for left, right in intervals + [interval_new]:
            heapq.heappush(heap, (left, START))
            heapq.heappush(heap, (right, END))

        result = []
        amount_open_intervals = 0
        left = None
        while heap:
            position, is_open = heapq.heappop(heap)

            if left is None:
                left = position

            amount_open_intervals += is_open
            if amount_open_intervals == 0:
                result.append([left, position])
                left = None

        return result
```
