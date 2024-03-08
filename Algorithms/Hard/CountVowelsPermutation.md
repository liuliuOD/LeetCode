![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1220. [Count Vowels Permutation](https://leetcode.com/problems/count-vowels-permutation)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 5/43) :
```python
MODULO = 1_000_000_007

class Solution:
    def countVowelPermutation(self, n: int) -> int:
        mapping = {
            'a': ['e',],
            'e': ['a', 'i',],
            'i': ['a', 'e', 'o', 'u',],
            'o': ['i', 'u',],
            'u': ['a',],
        }

        result = 0
        for key in mapping.keys():
            result = (result + self.dfs(key, n-1, mapping)) % MODULO

        return result

    def dfs(self, key: str, n: int, mapping: Dict[str, List[str]]) -> int:
        if n == 0:
            return 1

        result = 0
        for key_next in mapping[key]:
            result = (result + self.dfs(key_next, n-1, mapping)) % MODULO

        return result
```

Method 2 (DFS + Memoization (by Dictionary)) :
```python
MODULO = 1_000_000_007

class Solution:
    def countVowelPermutation(self, n: int) -> int:
        mapping = {
            'a': ['e',],
            'e': ['a', 'i',],
            'i': ['a', 'e', 'o', 'u',],
            'o': ['i', 'u',],
            'u': ['a',],
        }

        memoization = {}
        result = 0
        for vowel in mapping.keys():
            result = (result + self.dfs(vowel, n-1, memoization, mapping)) % MODULO

        return result

    def dfs(self, vowel: str, n: int, memoization: Dict[Tuple[int, str], int], mapping: Dict[str, List[str]]) -> int:
        key = (n, vowel)
        if key in memoization:
            return memoization[key]

        if n == 0:
            return 1

        result = 0
        for vowel_next in mapping[vowel]:
            result = (result + self.dfs(vowel_next, n-1, memoization, mapping)) % MODULO

        memoization[key] = result
        return result
```

Method 3 (DFS + Memoization (by List + Dictionary)) :
```python
MODULO = 1_000_000_007

class Solution:
    def countVowelPermutation(self, n: int) -> int:
        mapping = {
            'a': ['e',],
            'e': ['a', 'i',],
            'i': ['a', 'e', 'o', 'u',],
            'o': ['i', 'u',],
            'u': ['a',],
        }

        memoization = [{} for _ in range(n)]
        result = 0
        for vowel in mapping.keys():
            result = (result + self.dfs(vowel, n-1, memoization, mapping)) % MODULO

        return result

    def dfs(self, vowel: str, n: int, memoization: List[Dict[str, int]], mapping: Dict[str, List[str]]) -> int:
        if vowel in memoization[n]:
            return memoization[n][vowel]

        if n == 0:
            return 1

        result = 0
        for vowel_next in mapping[vowel]:
            result = (result + self.dfs(vowel_next, n-1, memoization, mapping)) % MODULO

        memoization[n][vowel] = result
        return result
```

Method 4 (Dynamic Programming, Space Complexity: $O(N)$ (N*5 = N)) :
```python
MODULO = 1_000_000_007

class Solution:
    def countVowelPermutation(self, n: int) -> int:
        mapping = {
            'a': ['e', 'i', 'u',],
            'e': ['a', 'i',],
            'i': ['e', 'o',],
            'o': ['i',],
            'u': ['i', 'o',],
        }

        dp = [{} for _ in range(n+1)]
        dp[1] = {key: 1 for key in mapping.keys()}
        for length in range(2, n+1):
            for key in mapping.keys():
                dp[length][key] = sum([dp[length-1][key_previous] for key_previous in mapping[key]]) % MODULO

        return sum(dp[n].values()) % MODULO
```

Method 5 (Dynamic Programming, Space Complexity: $O(N)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def countVowelPermutation(self, n: int) -> int:
        # record lists of vowels that should appear in front of each vowel
        mapping = {
            'a': ['e', 'i', 'u',],
            'e': ['a', 'i',],
            'i': ['e', 'o',],
            'o': ['i',],
            'u': ['i', 'o',],
        }

        # Space Optimization
        dp = {key: 1 for key in mapping.keys()}
        for length in range(2, n+1):
            temp = {}
            for key in mapping.keys():
                temp[key] = sum([dp[key_previous] for key_previous in mapping[key]]) % MODULO

            dp = temp

        return sum(dp.values()) % MODULO
```
