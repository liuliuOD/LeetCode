![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2746. [Decremental String Concatenation](https://leetcode.com/problems/maximize-the-confusion-of-an-exam)

### Solution :

Method 1 (Recursive, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def minimizeConcatenatedLength(self, words: List[str]) -> int:
        self.words = words
        return self.concate(words[0], 1)

    def concate(self, str_current: str, index_next: int) -> int:
        if index_next >= len(self.words):
            return len(str_current)

        str_next = self.words[index_next]
        str_current_next = str_current + str_next if str_current[-1] != str_next[0] else str_current[:-1] + str_next
        str_next_current = str_next + str_current if str_next[-1] != str_current[0] else str_next[:-1] + str_current

        return min(self.concate(str_current_next, index_next+1), self.concate(str_next_current, index_next+1))
```

Method 2 (Dynamic Programming + Memoization) :
```python
class Solution:
    def minimizeConcatenatedLength(self, words: List[str]) -> int:
        self.words = words
        self.memoization = defaultdict(int)

        return len(words[0]) + self.concate(1, words[0][0], words[0][-1])

    def concate(self, index: int, str_head: str, str_tail: str) -> int:
        if index >= len(self.words):
            return 0
        
        key_memoization = self.getMemoizationKey(index, str_head, str_tail)
        if key_memoization in self.memoization:
            return self.memoization[key_memoization]
        
        len_current = len(self.words[index])
        len_current_next = len_current + self.concate(index+1, str_head, self.words[index][-1])
        len_next_current = len_current + self.concate(index+1, self.words[index][0], str_tail)

        if str_tail == self.words[index][0]:
            len_current_next -= 1
        if self.words[index][-1] == str_head:
            len_next_current -= 1
        
        self.memoization[key_memoization] = min(len_current_next, len_next_current)

        return self.memoization[key_memoization]
    
    def getMemoizationKey(self, index: int, head: str, tail: str) -> str:
        return f'{index}-{head}-{tail}'
```
