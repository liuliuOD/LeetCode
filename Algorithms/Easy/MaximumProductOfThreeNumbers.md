![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 628. [Maximum Product Of Three Numbers](https://leetcode.com/problems/maximum-product-of-three-numbers)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$) :
```python
class Solution:
    def maximumProduct(self, nums: List[int]) -> int:
        min_heap = nums.copy()
        max_heap = [-num for num in nums]

        heapq.heapify(min_heap)
        heapq.heapify(max_heap)

        top_3 = [heapq.heappop(max_heap) for _ in range(3)]
        bottom_2 = [heapq.heappop(min_heap) for _ in range(2)]

        return max([-top_3[0]*top_3[1]*top_3[2], -top_3[0]*bottom_2[0]*bottom_2[1]])
```

Method 2 (Time Complexity: $O(N)$) :
```python
class Solution:
    def maximumProduct(self, nums: List[int]) -> int:
        top_3 = [-inf] * 3
        bottom_2 = [inf] * 2
        for num in nums:
            if num > top_3[2]:
                top_3[2], top_3[1], top_3[0] = num, top_3[2], top_3[1]
            elif num > top_3[1]:
                top_3[1], top_3[0] = num, top_3[1]
            elif num > top_3[0]:
                top_3[0] = num

            if num < bottom_2[0]:
                bottom_2[0], bottom_2[1] = num, bottom_2[0]
            elif num < bottom_2[1]:
                bottom_2[1] = num

        return max(reduce(lambda a, b: a*b, top_3, 1), top_3[-1]*bottom_2[0]*bottom_2[1])
```

Method 3 (Built-In method) :
```python
class Solution:
    def maximumProduct(self, nums: List[int]) -> int:
        nums.sort()

        multiply = lambda a, b: a*b
        return max(reduce(multiply, nums[-3:], 1), reduce(multiply, nums[:2]+[nums[-1]], 1))
```
