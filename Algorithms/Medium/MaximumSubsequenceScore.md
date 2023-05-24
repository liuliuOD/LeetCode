![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2542. [Maximum Subsequence Score](https://leetcode.com/problems/maximum-subsequence-score)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def maxScore(self, nums1: List[int], nums2: List[int], k: int) -> int:
        self.nums1 = nums1
        self.nums2 = nums2
        result = 0
        for id_n1 in range(len(nums1)):
            result = max(result, self.dfs([id_n1], k - 1))
        return result

    def dfs(self, ids, step) -> int:
        result = 0
        if step == 0:
            min_num2 = 10**5
            for id in ids:
                result += self.nums1[id]
                min_num2 = min(min_num2, self.nums2[id])
            return result * min_num2

        for i in range(ids[-1] + 1, len(self.nums1)):
            result = max(result, self.dfs(ids + [i], step - 1))
        return result
```

Method 2 (Heap) :
```python
class Solution:
    def maxScore(self, nums1: List[int], nums2: List[int], k: int) -> int:
        group = zip(nums1, nums2)
        group = sorted(group, key=lambda item: -item[-1])

        min_heap = []
        temp = 0
        result = 0
        for pair in group:
            n1, n2 = pair
            heappush(min_heap, n1)
            temp += n1
            if len(min_heap) > k:
                temp -= heappop(min_heap)
            if len(min_heap) == k:
                result = max(result, temp * n2)

        return result
```
