![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 719. [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance)

### Solution :

Method 1 (Brute Force + Binary Heap, ERROR: "Time Limit Exceeded", 16/19, Time Complexity: $O(N^2*Log(K))$, Space Complexity: $O(K)$ (N: number of the elements in `nums`, K: value of `k`)) :
```python
class Solution:
    def smallestDistancePair(self, nums: List[int], k: int) -> int:
        heap = []
        for a, b in combinations(nums, 2):
            heapq.heappush(heap, -abs(a-b))
            if len(heap) > k:
                heapq.heappop(heap)

        return -heapq.heappop(heap)
```

Method 2 (Brute Force + Bucket Sort, Time Complexity: $O(N^2 + M)$, Space Complexity: $O(M)$ (N: number of the elements in `nums`, M: the maximum value in `nums`)) :
```python
class Solution:
    def smallestDistancePair(self, nums: List[int], k: int) -> int:
        buckets = [0] * (max(nums) + 1)
        for a, b in combinations(nums, 2):
            buckets[abs(a-b)] += 1

        for distance in range(len(buckets)):
            k -= buckets[distance]

            if k <= 0:
                return distance

        # unreachable
        return -1
```
