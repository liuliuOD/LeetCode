![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)

### Solution :

Method 1 (Two Pointer) :
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        if n == 0:
            return 0

        mapping = defaultdict(int)
        result = 1
        left = right = 0
        while right < n:
            char_current = s[right]
            mapping[char_current] += 1
            while mapping[char_current] > 1:
                mapping[s[left]] -= 1
                left += 1

            result = max(result, right - left + 1)
            right += 1
        return result
```
