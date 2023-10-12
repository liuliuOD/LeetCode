![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 139. [Word Break](https://leetcode.com/problems/word-break)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 32/46) :
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        len_s = len(s)
        positions = set()
        for word in wordDict:
            if word not in s:
                continue

            len_word = len(word)
            pointer_left = pointer_right = 0
            while pointer_left <= pointer_right and pointer_right < len_s:
                index_word = pointer_right - pointer_left
                if index_word >= len_word or s[pointer_right] != word[index_word]:
                    pointer_left += 1
                    pointer_right = pointer_left
                    continue
                if len_word == (pointer_right - pointer_left + 1):
                    positions.add(tuple(range(pointer_left, pointer_right+1)))

                pointer_right += 1

        return self.dfs([], set(), len_s, list(positions))

    def dfs(self, choose_position: List[int], mask: Set[int], len_s: int, positions: List[Tuple[int]]) -> bool:
        if len(choose_position) == len_s:
            return True

        for index in range(len(positions)):
            if index in mask:
                continue
            if any(index_exist in positions[index] for index_exist in choose_position):
                continue

            mask_next = mask.copy()
            mask_next.add(index)
            if self.dfs(choose_position+list(positions[index]), mask_next, len_s, positions):
                return True

        return False
```

Method 2 (DFS + Memoization, ERROR: "Time Limit Exceeded", 34/46) :
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        len_s = len(s)
        positions = set()
        for word in wordDict:
            if word not in s:
                continue

            len_word = len(word)
            pointer_left = pointer_right = 0
            while pointer_left <= pointer_right and pointer_right < len_s:
                index_word = pointer_right - pointer_left
                if index_word >= len_word or s[pointer_right] != word[index_word]:
                    pointer_left += 1
                    pointer_right = pointer_left
                    continue
                if (pointer_right - pointer_left + 1) == len_word:
                    positions.add(tuple(range(pointer_left, pointer_right+1)))

                pointer_right += 1

        self.memoization = {}
        return self.dfs([], set(), len_s, list(positions))

    def dfs(self, choose_position: List[int], mask: Set[int], len_s: int, positions: List[Tuple[int]]) -> bool:
        if len(choose_position) == len_s:
            return True

        mask_tuple = tuple(mask)
        if mask_tuple in self.memoization:
            return self.memoization[mask_tuple]

        for index in range(len(positions)):
            if index in mask:
                continue
            if any(index_exist in positions[index] for index_exist in choose_position):
                continue

            mask_next = mask.copy()
            mask_next.add(index)
            if self.dfs(choose_position+list(positions[index]), mask_next, len_s, positions):
                return True

        self.memoization[mask_tuple] = False
        return self.memoization[mask_tuple]
```

Method 3 (DFS + Memoization, ERROR: "Time Limit Exceeded", 35/46) :
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        len_s = len(s)
        positions = set()
        for word in wordDict:
            if word not in s:
                continue

            len_word = len(word)
            pointer_left = pointer_right = 0
            while pointer_left <= pointer_right and pointer_right < len_s:
                index_word = pointer_right - pointer_left
                if index_word >= len_word or s[pointer_right] != word[index_word]:
                    pointer_left += 1
                    pointer_right = pointer_left
                    continue
                if (pointer_right - pointer_left + 1) == len_word:
                    positions.add(tuple(range(pointer_left, pointer_right+1)))

                pointer_right += 1

        self.memoization = {}
        return self.dfs([], set(), len_s, sorted(list(positions), key=lambda position: len(position), reverse=True))

    def dfs(self, choose_position: List[int], mask: Set[int], len_s: int, positions: List[Tuple[int]]) -> bool:
        if len(choose_position) == len_s:
            return True

        mask_tuple = tuple(mask)
        if mask_tuple in self.memoization:
            return self.memoization[mask_tuple]

        for index in range(len(positions)):
            if index in mask:
                continue
            if any(index_exist in positions[index] for index_exist in choose_position):
                continue

            mask_next = mask.copy()
            mask_next.add(index)
            if self.dfs(choose_position+list(positions[index]), mask_next, len_s, positions):
                return True

        self.memoization[mask_tuple] = False
        return self.memoization[mask_tuple]
```

Method 4 (DFS + Memoization, ERROR: "Time Limit Exceeded", 38/46) :
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        len_s = len(s)
        positions: Set[Tuple[int]] = set()
        positions_exist: Set[int] = set()
        for word in wordDict:
            if word not in s:
                continue

            len_word = len(word)
            pointer_left = pointer_right = 0
            while pointer_left <= pointer_right and pointer_right < len_s:
                index_word = pointer_right - pointer_left
                if index_word >= len_word or s[pointer_right] != word[index_word]:
                    pointer_left += 1
                    pointer_right = pointer_left
                    continue
                if (pointer_right - pointer_left + 1) == len_word:
                    position = range(pointer_left, pointer_right+1)
                    positions_exist = positions_exist.union(set(position))
                    positions.add(tuple(position))

                pointer_right += 1
        
        if len(positions_exist) != len_s:
            return False

        self.memoization = {}
        return self.dfs([], set(), len_s, sorted(list(positions), key=lambda position: len(position), reverse=True))

    def dfs(self, choose_position: List[int], mask: Set[int], len_s: int, positions: List[Tuple[int]]) -> bool:
        if len(choose_position) == len_s:
            return True

        mask_tuple = tuple(mask)
        if mask_tuple in self.memoization:
            return self.memoization[mask_tuple]

        for index in range(len(positions)):
            if index in mask:
                continue
            if any(index_exist in positions[index] for index_exist in choose_position):
                continue

            mask_next = mask.copy()
            mask_next.add(index)
            if self.dfs(choose_position+list(positions[index]), mask_next, len_s, positions):
                return True

        self.memoization[mask_tuple] = False
        return self.memoization[mask_tuple]
```

Method 5 (DFS + Memoization) :
```python
class Solution:
    def wordBreak(self, s: str, word_dict: List[str]) -> bool:
        memoization = dict()
        return self.dfs(s, memoization, set(word_dict))

    def dfs(self, s: str, memoization: Dict[str, bool], word_set: Set[str]) -> bool:
        if s in memoization:
            return memoization[s]

        if s in word_set:
            return True

        for index in range(1, len(s)):
            substring = s[:index]
            if substring in word_set and self.dfs(s[index:], memoization, word_set):
                memoization[s] = True
                return memoization[s]

        memoization[s] = False
        return memoization[s]
```

Method 6 (DFS + Memoization) :
```python
class Solution:
    def wordBreak(self, s: str, word_dict: List[str]) -> bool:
        word_dict = set(word_dict)
        memoization: Dict[str, bool] = {}
        return self.dfs(s, memoization, word_dict)

    def dfs(self, s: str, memoization: Dict[str, bool], word_dict: Set[str]) -> bool:
        if s in memoization:
            return memoization[s]

        if s == '':
            return True

        result = False
        for index in range(len(s)):
            if s[:index+1] not in word_dict:
                continue

            result |= self.dfs(s[index+1:], memoization, word_dict)
            if result:
                break

        memoization[s] = result
        return result
```

Method 7 (Dynamic Programming) :
```python
class Solution:
    def wordBreak(self, s: str, word_dict: List[str]) -> bool:
        n = len(s)
        word_dict = set(word_dict)
        dp = [False] * (n+1)
        dp[0] = True
        for amount in range(1, n+1):
            for amount_current in range(1, amount+1):
                if s[amount-amount_current:amount] in word_dict:
                    dp[amount] = dp[amount-amount_current]
                if dp[amount]:
                    break

        return dp[n]
```
