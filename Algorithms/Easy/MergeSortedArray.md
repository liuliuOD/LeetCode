![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 88. [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array)

### Solution :

```python
"""
Do not return anything, modify nums1 in-place instead.
"""
```

Method 1 (Heap, Time Complexity: $O(N*Log(N))$) :
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        heap = nums1[:m] + nums2[:n]
        heapq.heapify(heap)
        for index in range(m+n):
            nums1[index] = heapq.heappop(heap)
```

Method 2 (Two Pointer, Time Complexity: $O(M+N)$) :
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        index = m + n - 1
        pointer_m = m - 1
        pointer_n = n - 1

        # Option 1
        while pointer_m >= 0 and pointer_n >= 0:
            if nums1[pointer_m] >= nums2[pointer_n]:
                nums1[index] = nums1[pointer_m]
                pointer_m -= 1
            else:
                nums1[index] = nums2[pointer_n]
                pointer_n -= 1

            index -= 1

        while pointer_n >= 0:
            nums1[index] = nums2[pointer_n]
            pointer_n -= 1
            index -= 1
        """
        # Option 2

        while pointer_n >= 0:
            if pointer_m >= 0 and nums1[pointer_m] >= nums2[pointer_n]:
                nums1[index] = nums1[pointer_m]
                pointer_m -= 1
            else:
                nums1[index] = nums2[pointer_n]
                pointer_n -= 1

            index -= 1
        """
```
