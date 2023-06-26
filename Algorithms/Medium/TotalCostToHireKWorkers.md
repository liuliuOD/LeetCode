![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2462. [Total Cost To Hire K Workers](https://leetcode.com/problems/total-cost-to-hire-k-workers)

### Solution :

Method 1 (Two Pointer + Heap) :
```python
class Solution:
    def totalCost(self, costs: List[int], k: int, candidates: int) -> int:
        result = 0
        pointer_left = 0
        pointer_right = len(costs)
        heap_group_left = []
        heap_group_right = []

        while k > 0:
            while pointer_left < pointer_right and len(heap_group_left) < candidates:
                heapq.heappush(heap_group_left, costs[pointer_left])
                pointer_left += 1
            
            while pointer_left < pointer_right and len(heap_group_right) < candidates:
                pointer_right -= 1
                heapq.heappush(heap_group_right, costs[pointer_right])

            top_group_left = heap_group_left[0] if len(heap_group_left) else float('inf')
            top_group_right = heap_group_right[0] if len(heap_group_right) else float('inf')

            if top_group_left <= top_group_right:
                result += heapq.heappop(heap_group_left)
            else:
                result += heapq.heappop(heap_group_right)

            k -= 1

        return result
```
