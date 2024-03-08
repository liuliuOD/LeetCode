![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2971. [Find Polygon With The Largest Perimeter](https://leetcode.com/problems/find-polygon-with-the-largest-perimeter)

### Solution :

Method 1 (Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def largestPerimeter(self, nums: List[int]) -> int:
        result = -1
        perimeter = 0
        for num in sorted(nums):
            if perimeter > num:
                result = perimeter + num

            perimeter += num

        return result
```

Method 2 (Reverse Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def largestPerimeter(self, nums: List[int]) -> int:
        nums.sort(reverse=True)
        perimeter = sum(nums)
        for num in nums:
            perimeter -= num
            if perimeter > num:
                return perimeter + num

        return -1
```

Method 3 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def largestPerimeter(self, nums: List[int]) -> int:
        result = -1
        perimeter = 0
        heapq.heapify(nums)
        while nums:
            num = heapq.heappop(nums)
            if perimeter > num:
                result = perimeter + num

            perimeter += num

        return result
```
