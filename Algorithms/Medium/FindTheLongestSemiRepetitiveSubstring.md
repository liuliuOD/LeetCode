![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2730. [Find The Longest Semi-Repetitive Substring](https://leetcode.com/problems/find-the-longest-semi-repetitive-substring)

### Solution :

Method 1 (In biweekly contest 106) :
```python
class Solution:
    def longestSemiRepetitiveSubstring(self, s: str) -> int:
        last = None
        pairs = {'start': 0, 'end': 0}
        consecutive_times = 0
        temp = 0
        result = 0
        for index, ch in enumerate(s):
            if last == ch:
                if consecutive_times == 1:
                    result = max(result, temp)
                    temp = temp - (pairs['end'] - pairs['start'])
                pairs['start'], pairs['end'] = pairs['end'], index
                consecutive_times = 1

            temp += 1
            last = ch
        result = max(result, temp)
        return result
```

Method 2 :
```python
class Solution:
    def longestSemiRepetitiveSubstring(self, s: str) -> int:
        substring_start = 0
        previous_repetitive_end = -1
        result = 1
        for index in range(1, len(s)):
            if s[index] == s[index - 1]:
                if previous_repetitive_end > 0:
                    substring_start = previous_repetitive_end
                previous_repetitive_end = index
            result = max(result, index - substring_start + 1)
        return result
```
