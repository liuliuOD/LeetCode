![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 392. [Is Subsequence](https://leetcode.com/problems/is-subsequence)

### Solution :

Method 1 (Adjust List + Brute Force) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        mapping = defaultdict(list)
        for index_t, ch_t in enumerate(t):
            for ch_s in s:
                if ch_s == ch_t:
                    mapping[ch_s].append(index_t)
        
        temp = -1
        for ch_s in s:
            if ch_s not in mapping:
                return False

            heapq.heapify(mapping[ch_s])
            while mapping[ch_s]:
                index_s = heapq.heappop(mapping[ch_s])
                if index_s > temp:
                    temp = index_s
                    break

                if len(mapping[ch_s]) == 0:
                    return False
        return True
```

Method 2 (Two Pointer) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        if len(s) == 0:
            return True

        pointer_s = 0
        for ch_t in t:
            if ch_t == s[pointer_s]:
                pointer_s += 1
            if pointer_s == len(s):
                return True
        return False
```

Method 3 (Two Pointer + add default string `=`) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        s = '=' + s
        t = '=' + t
        pointer_s = 0
        for ch_t in t:
            if pointer_s < len(s) and ch_t == s[pointer_s]:
                pointer_s += 1
            if pointer_s == len(s):
                return True
        return False
```

Method 4 (Dynamic Programming) :
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        len_s = len(s)
        len_t = len(t)
        # add '=' to position 0, to set init status when either `s` or `t` is empty string
        s = '=' + s
        t = '=' + t
        memoization = [[1] + [0] * len_s for _ in range(len_t+1)]

        for index_t, index_s in product(range(1, len_t+1), range(1, len_s+1)):
            memoization[index_t][index_s] = memoization[index_t-1][index_s-1] if t[index_t] == s[index_s] else memoization[index_t-1][index_s]
        
        return memoization[-1][-1]
```
