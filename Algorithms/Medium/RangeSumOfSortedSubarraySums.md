![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1508. [Range Sum Of Sorted Subarray Sums](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums)

### Solution :

Method 1 (Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def rangeSum(self, nums: List[int], n: int, left: int, right: int) -> int:
        array = []
        for index, num in enumerate(nums):
            summarization = 0
            for index_previous in reversed(range(index+1)):
                summarization += nums[index_previous]
                array.append(summarization)

        array.sort()
        return sum(array[left-1:right]) % 1_000_000_007
```

Method 2 (Binary Heap, Time Complexity: $O(N^2*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rangeSum(self, nums: List[int], n: int, left: int, right: int) -> int:
        heap = [(num, index) for index, num in enumerate(nums)]
        heapq.heapify(heap)

        result = 0
        for amount_pop in range(1, right+1):
            num, index = heapq.heappop(heap)
            if amount_pop >= left:
                result = (result + num) % 1_000_000_007

            if index < n-1:
                heapq.heappush(heap, (num+nums[index+1], index+1))

        return result
```
