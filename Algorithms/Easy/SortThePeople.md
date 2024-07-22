![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2418. [Sort The People](https://leetcode.com/problems/sort-the-people)

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sortPeople(self, names: List[str], heights: List[int]) -> List[str]:
        n = len(names)
        index_ordered = sorted(range(n), key=lambda index: heights[index], reverse=True)

        return [names[index] for index in index_ordered]
```
