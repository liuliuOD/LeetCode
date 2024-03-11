![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 791. [Custom Sort String](https://leetcode.com/problems/custom-sort-string)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def customSortString(self, order: str, s: str) -> str:
        counter = Counter(s)
        result = ''
        for key in order:
            if key not in counter.keys():
                continue

            result += key * counter[key]
            del counter[key]

        for key, amount in counter.items():
            result += key * amount

        return result
```
