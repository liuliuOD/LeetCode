![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 41. [First Missing Positive](https://leetcode.com/problems/first-missing-positive)

### Constraints:

- Runs in $O(N)$ time.
- Uses $O(1)$ auxiliary space.

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums_set = set(nums)
        for candidate in range(1, len(nums_set)+2):
            if candidate in nums_set:
                continue

            return candidate
```
