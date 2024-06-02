![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3170. [Lexicographically Minimum String After Removing Stars](https://leetcode.com/problems/lexicographically-minimum-string-after-removing-stars)

### Solution :

Method 1 (In weekly contest 400, Hash Map + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def clearStars(self, s: str) -> str:
        mapping = defaultdict(list)
        candidates: set[int] = set()
        for index, char in enumerate(s):
            mapping[char].append(index)
            if char != "*":
                candidates.add(char)

        mapping["*"].reverse()
        char_ordered = sorted(list(candidates), reverse=True)
        while mapping["*"]:
            index = mapping["*"].pop()

            index_char = len(char_ordered) - 1
            while len(mapping.get(char_ordered[index_char], 0)) == 0 or mapping[char_ordered[index_char]][0] >= index:
                index_char -= 1

            char_current = char_ordered[index_char]
            left, right = 0, len(mapping[char_current])-1
            while left <= right:
                middle = left + (right-left)//2
                if mapping[char_current][middle] <= index:
                    left = middle + 1
                else:
                    right = middle - 1

            mapping[char_current].pop(right)
            if len(mapping[char_current]) == 0:
                char_ordered.pop(index_char)

        result = [0] * len(s)
        for char, group_index in mapping.items():
            for index in group_index:
                result[index] = char

        return "".join(filter(lambda a: a != 0, result))
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def clearStars(self, s: str) -> str:
        mapping = defaultdict(list)
        for index, char in enumerate(s):
            if char == "*":
                char_minimum = min(mapping.keys())
                mapping[char_minimum].pop()
                if len(mapping[char_minimum]) == 0:
                    del mapping[char_minimum]
            else:
                mapping[char].append(index)

        result = [""] * len(s)
        for char, positions in mapping.items():
            for index in positions:
                result[index] = char
        return "".join(filter(lambda value: value != "", result))
```
