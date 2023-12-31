![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1624. [Largest Substring Between Two Equal Characters](https://leetcode.com/problems/largest-substring-between-two-equal-characters)

### Solution :

Method 1 (Hash Map) :
```python
class Solution:
    def maxLengthBetweenEqualCharacters(self, s: str) -> int:
        mapping = defaultdict(list)
        for index, char in enumerate(s):
            mapping[char].append(index)

        result = -1
        for group in mapping.values():
            if len(group) <= 1:
                continue

            result = max(result, group[-1] - group[0] - 1)

        return result
```

Method 2 (Array) :
```python
BASE = ord('a')

class Solution:
    def maxLengthBetweenEqualCharacters(self, s: str) -> int:
        mapping = [[] for _ in range(26)]
        # Option 1
        for index, char in enumerate(s):
            mapping[ord(char)-BASE].append(index)

        result = -1
        for group in mapping:
            if len(group) <= 1:
                continue

            result = max(result, group[-1] - group[0] - 1)
        """
        # Option 2

        result = -1
        for index, char in enumerate(s):
            mapping[ord(char)-BASE].append(index)
            if len(mapping[ord(char)-BASE]) <= 1:
                continue

            result = max(result, mapping[ord(char)-BASE][-1] - mapping[ord(char)-BASE][0] - 1)
        """

        return result
```
