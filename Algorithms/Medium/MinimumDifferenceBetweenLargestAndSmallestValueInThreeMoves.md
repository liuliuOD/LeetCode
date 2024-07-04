![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1509. [Minimum Difference Between Largest And Smallest Value In Three Moves](https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves)

### Solution :

Method 1 (Brute Force + Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minDifference(self, nums: List[int]) -> int:
        n = len(nums)
        if n <= 3:
            return 0

        nums.sort()
        result = inf
        for amount_left in range(4):
            amount_right = 4 - amount_left
            result = min(result, nums[n-amount_right]-nums[amount_left])

        return result
```

Method 2 (Binary Heap + Space Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minDifference(self, nums: List[int]) -> int:
        n = len(nums)
        if n <= 4:
            return 0

        max_heap, min_heap = heapq.nlargest(4, nums), heapq.nsmallest(4, nums)

        min_heap.sort()
        max_heap.sort()
        result = inf
        for offset in range(4):
            result = min(result, max_heap[offset] - min_heap[offset])

        return result
```
