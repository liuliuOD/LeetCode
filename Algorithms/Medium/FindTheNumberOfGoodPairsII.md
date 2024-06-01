![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2761. [Find The Number Of Good Pairs II](https://leetcode.com/problems/find-the-number-of-good-pairs-ii)

### Solution :

Method 1 (In weekly contest 399, Time Complexity: $O(N+M*{(maximum-minimum) \over K})$ (N: amount of elements in `nums1`, M: amount of elements in `nums2`, K: the value of `k`, maximum: the maximum value in `nums1`, minimum: the minimum value in `nums1`), Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfPairs(self, nums1: List[int], nums2: List[int], k: int) -> int:

        counter = Counter(nums1)
        minimum = min(nums1)
        maximum = max(nums1)
        result = 0
        for num in nums2:
            base = num * k
            multiply = 1 + (minimum - 1) // base
            while base * multiply <= maximum:
                target = base * multiply
                if target in counter:
                    result += counter[target]

                multiply += 1

        return result
```
