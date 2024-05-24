![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1255. [Maximum Score Words Formed By Letters](https://leetcode.com/problems/maximum-score-words-formed-by-letters)

### Solution :

Method 1 (Bitmask + Hash Map) :
```python
BASE = ord('a')

class Solution:
    def maxScoreWords(self, words: List[str], letters: List[str], score: List[int]) -> int:
        counter = Counter(letters)
        n = len(words)
        result = 0
        for bitmask in range(1, 1<<n):
            counter_current = defaultdict(int)
            for index in range(n):
                if (1 << index) & bitmask == 0:
                    continue

                for char in words[index]:
                    counter_current[char] += 1

            current_score = 0
            for char in counter_current.keys():
                if char not in counter or counter[char] < counter_current[char]:
                    break

                current_score += counter_current[char] * score[ord(char) - BASE]
            else:
                result = max(result, current_score)

        return result
```
