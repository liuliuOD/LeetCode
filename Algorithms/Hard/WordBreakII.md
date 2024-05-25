![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 140. [Word Break II](https://leetcode.com/problems/word-break-ii)

### Solution :

Method 1 (Bitmask + Hash Set) :
```python
class Solution:
    def wordBreak(self, s: str, word_dict: List[str]) -> List[str]:
        n = len(s)
        word_dict: set[str] = set(word_dict)
        result: list[str] = []
        for bitmask in range(1<<(n-1)):
            elements: list[str] = []
            index_start = 0
            for index_end in range(n):
                if (1<<index_end) & bitmask == 0:
                    continue

                if s[index_start:index_end+1] not in word_dict:
                    break

                elements.append(s[index_start:index_end+1])
                index_start = index_end + 1
            else:
                if index_start < n and s[index_start:] not in word_dict:
                    continue

                elements.append(s[index_start:])
                result.append(" ".join(elements))

        return result
```

Method 2 (Backtracking + Hash Set) :
```python
class Solution:
    def wordBreak(self, s: str, word_dict: List[str]) -> List[str]:
        n = len(s)
        candidates: set[str] = set(word_dict)
        self.result: list[str] = []

        self.backtracking(0, 0, [], candidates, s)
        return self.result

    def backtracking(self, index_start: int, index_end: int, words: list[str], candidates: set[str], s: str):
        n = len(s)
        if index_end >= n:
            current: str = s[index_start:]
            if current in candidates:
                words.append(current)
                self.result.append(" ".join(words))
                words.pop()
            return

        self.backtracking(index_start, index_end+1, words, candidates, s)

        current: str = s[index_start:index_end+1]
        if current in candidates:
            words.append(current)
            self.backtracking(index_end+1, index_end+1, words, candidates, s)
            words.pop()
```
