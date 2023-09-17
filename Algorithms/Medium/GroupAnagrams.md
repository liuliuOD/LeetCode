![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 49. [Group Anagrams](https://leetcode.com/problems/group-anagrams)

### Solution :

Method 1 (Hash Map) :
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mapping = defaultdict(list)

        for string in strs:
            mapping[''.join(sorted(string))].append(string)

        return mapping.values()
```
