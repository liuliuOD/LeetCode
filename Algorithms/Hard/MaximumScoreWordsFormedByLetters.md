![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1255. [Maximum Score Words Formed By Letters](https://leetcode.com/problems/maximum-score-words-formed-by-letters)

### Solution :

Method 1 (Bitmask + Hash Map, Time Complexity: $O(M*N*2^N)$ (M: maximum length of each element in `words`, N: length of `words`), Space Complexity; $O(1)$) :
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

Method 2 (DFS + Hash Map, Time Complexity: $O(M*N*2^N)$ (M: maximum length of each element in `words`, N: length of `words`), Space Complexity; $O(1)$):
```python
BASE = ord('a')

class Solution:
    def maxScoreWords(self, words: List[str], letters: List[str], score: List[int]) -> int:
        counter = Counter(letters)
        self.result = 0

        self.dfs(0, defaultdict(int), counter, words, score)

        return self.result

    def dfs(self, index: int, counter_cumulative: dict[str, int], counter_target: dict[str, int], words, score):
        n = len(words)
        if index >= n:
            score_current = 0
            for char in counter_cumulative.keys():
                if counter_cumulative[char] == 0:
                    continue

                if char not in counter_target or counter_target[char] < counter_cumulative[char]:
                    break

                score_current += counter_cumulative[char] * score[ord(char)-BASE]
            else:
                self.result = max(self.result, score_current)

            return

        self.dfs(index+1, counter_cumulative, counter_target, words, score)

        counter_temp = defaultdict(int)
        for char in words[index]:
            counter_temp[char] += 1
        else:
            for char in counter_temp.keys():
                counter_cumulative[char] += counter_temp[char]

            self.dfs(index+1, counter_cumulative, counter_target, words, score)

            for char in counter_temp.keys():
                counter_cumulative[char] -= counter_temp[char]
```

Method 3 (DFS + Hash Map, Time Complexity: $O(M*N*2^N)$ (M: maximum length of each element in `words`, N: length of `words`), Space Complexity; $O(1)$):
```python
BASE = ord('a')

class Solution:
    def maxScoreWords(self, words: List[str], letters: List[str], score: List[int]) -> int:
        counter = Counter(letters)
        self.result = 0

        self.dfs(0, defaultdict(int), counter, words, score)

        return self.result

    def dfs(self, index: int, counter_cumulative: dict[str, int], counter_target: dict[str, int], words, score):
        n = len(words)
        if index >= n:
            score_current = 0
            for char in counter_cumulative.keys():
                if counter_cumulative[char] == 0:
                    continue

                if char not in counter_target or counter_target[char] < counter_cumulative[char]:
                    break

                score_current += counter_cumulative[char] * score[ord(char)-BASE]
            else:
                self.result = max(self.result, score_current)

            return

        self.dfs(index+1, counter_cumulative, counter_target, words, score)

        counter_temp = defaultdict(int)
        for char in words[index]:
            counter_temp[char] += 1
            if counter_cumulative[char] + counter_temp[char] > counter_target[char]:
                break
        else:
            for char in counter_temp.keys():
                counter_cumulative[char] += counter_temp[char]

            self.dfs(index+1, counter_cumulative, counter_target, words, score)

            for char in counter_temp.keys():
                counter_cumulative[char] -= counter_temp[char]
```
