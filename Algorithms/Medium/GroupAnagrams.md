![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 49. [Group Anagrams](https://leetcode.com/problems/group-anagrams)

### Solution :

Method 1 (Hash Map + Hash Set, ERROR: "Time Limit Exceeded", 111/120) :
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        n = len(strs)
        visited = set()
        result = []
        for index in range(n):
            if index in visited:
                continue
            visited.add(index)

            result.append([strs[index]])
            counter_target = Counter(strs[index])
            for index_current in range(index+1, n):
                if index_current in visited:
                    continue

                counter_current = Counter(strs[index_current])
                set_current = set(counter_current.keys())
                set_target = set(counter_target.keys())
                if (len(set_current - set_target) != len(set_target - set_current)) or (len(set_current - set_target) == len(set_target - set_current) and len(set_current - set_target) != 0):
                    continue

                for key, amount in counter_target.items():
                    if amount != counter_current[key]:
                        break
                else:
                    result[-1].append(strs[index_current])
                    visited.add(index_current)

        return result
```

Method 2 (Hash Map) :
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mapping = defaultdict(list)

        for string in strs:
            mapping[''.join(sorted(string))].append(string)

        return mapping.values()
```

Method 3 (Hash Map) :
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        result = defaultdict(list)
        for string in strs:
            result[tuple(sorted(string))].append(string)

        return result.values()
```
