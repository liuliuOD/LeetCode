![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1438. [Longest Continuous Subarray With Absolute Diff Less Than Or Equal To Limit](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit)

### Solution :

Method 1 (Sliding Window + Binary Search, ERROR: "Time Limit Exceeded", 56/61, Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        n = len(nums)
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left)//2
            result = False
            ordered = []
            for index in range(n):
                bisect.insort_left(ordered, nums[index])
                if index >= middle:
                    index_remove = bisect.bisect_left(ordered, nums[index-middle])
                    ordered.pop(index_remove)

                if index >= middle-1 and ordered[-1]-ordered[0] <= limit:
                    result = True
                    break

            if result:
                left = middle + 1
            else:
                right = middle - 1

        return right
```

Method 2 (Sliding Window + Binary Heap, Time Complexity: $O(N*(Log(N))^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        n = len(nums)
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left)//2
            heap_max = []
            heap_min = []
            result = False
            for index in range(n):
                heapq.heappush(heap_max, (-nums[index], index))
                heapq.heappush(heap_min, (nums[index], index))
                if index >= middle:
                    while heap_max[0][1] <= index-middle:
                        heapq.heappop(heap_max)
                    while heap_min[0][1] <= index-middle:
                        heapq.heappop(heap_min)

                if index >= middle-1 and -heap_max[0][0]-heap_min[0][0] <= limit:
                    result = True
                    break

            if result:
                left = middle + 1
            else:
                right = middle - 1

        return right
```
