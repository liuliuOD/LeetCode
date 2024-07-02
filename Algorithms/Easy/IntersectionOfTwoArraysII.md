![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 350. [Intersection Of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii)

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: number of the elements in `nums1`, N: number of the elements in `nums2`)) :
```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        counter = Counter(nums1)
        result: list[int] = []
        for num in nums2:
            if num in counter and counter[num]:
                counter[num] -= 1
                result.append(num)

        return result
```
