![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1750. [Minimum Length Of String After Deleting Similar Ends](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minimumLength(self, s: str) -> int:
        left = 0
        right = len(s) - 1
        while left < right and s[left] == s[right]:
            target_right = s[right]
            target_left = s[left]
            while left < right and s[left] == target_right:
                left += 1
            while left <= right and s[right] == target_left:
                right -= 1

        return 0 if right < left else right - left + 1
```
