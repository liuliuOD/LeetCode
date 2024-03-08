![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1425. [Constrained Subsequence Sum](https://leetcode.com/problems/constrained-subsequence-sum)

### Solution :

Method 1 (Dynamic Programming, ERROR: "Time Limit Exceeded", 20/36, Time Complexity: $O(N*K)$ (N: length of `nums`, K: value of `k`)) :
```python
class Solution:
    def constrainedSubsetSum(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp= [-inf] * n
        for index in range(n):
            dp[index] = nums[index]
            for offset in range(1, k+1):
                if index-offset < 0:
                    continue

                dp[index] = max(dp[index], nums[index]+dp[index-offset])

        return max(dp)
```

Method 2 (Binary Heap) :
```python
class Solution:
    def constrainedSubsetSum(self, nums: List[int], k: int) -> int:
        n = len(nums)
        heap = []
        results= [-inf] * n
        for index in range(n):
            results[index] = nums[index]

            while heap:
                maximum, index_maximum = heapq.heappop(heap)
                maximum = -maximum

                # drop this item if index_maximum out of the valid range
                if index_maximum < index-k:
                    continue
                
                heapq.heappush(heap, (-maximum, index_maximum))
                results[index] = max(results[index], nums[index] + maximum)
                break

            heapq.heappush(heap, (-results[index], index))

        return max(results)
```
