![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 712. [Minimum ASCII Delete Sum For Two Strings](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings)

### Solution :

Method 1 (DFS + Set, ERROR: "Time Limit Exceeded", 27/93) :
```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        equal_sum = set([])
        self.getEqualList(equal_sum, s1, s2, 0)

        return min(equal_sum)

    def getEqualList(self, equal_sum: Set[int], s1: str, s2: str, sum_value: int):
        if len(s1) == len(s2) == 0:
            equal_sum.add(sum_value)
        elif len(s1) == 0:
            equal_sum.add(sum_value+sum([ord(value) for value in s2]))
        elif len(s2) == 0:
            equal_sum.add(sum_value+sum([ord(value) for value in s1]))

        if s1[0] == s2[0]:
            self.getEqualList(equal_sum, s1[1:], s2[1:], sum_value)
            return None

        self.getEqualList(equal_sum, s1[1:], s2, sum_value+ord(s1[0]))
        self.getEqualList(equal_sum, s1, s2[1:], sum_value+ord(s2[0]))
```

Method 2 (DFS + Return-Minimum, ERROR: "Time Limit Exceeded", 27/93) :
```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        return self.getEqualList(s1, s2)

    def getEqualList(self, s1: str, s2: str) -> int:
        if len(s1) == len(s2) == 0:
            return 0
        elif len(s1) == 0:
            return sum([ord(value) for value in s2])
        elif len(s2) == 0:
            return sum([ord(value) for value in s1])

        if s1[0] == s2[0]:
            sum_value = self.getEqualList(s1[1:], s2[1:])
        else:
            sum_value = min(ord(s1[0]) + self.getEqualList(s1[1:], s2), ord(s2[0]) + self.getEqualList(s1, s2[1:]))

        return sum_value
```

Method 3 (DFS + Memoization) :
```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        memoization: Dict[str, Dict[str, int]] = defaultdict(dict)
        return self.getEqualList(s1, s2, memoization)

    def getEqualList(self, s1: str, s2: str, memoization: Dict[str, Dict[str, int]]) -> int:
        if s1 in memoization and s2 in memoization[s1]:
            return memoization[s1][s2]

        if len(s1) == len(s2) == 0:
            return 0
        elif len(s1) == 0:
            return sum([ord(value) for value in s2])
        elif len(s2) == 0:
            return sum([ord(value) for value in s1])

        if s1[0] == s2[0]:
            sum_value = self.getEqualList(s1[1:], s2[1:], memoization)
        else:
            sum_value = min(ord(s1[0]) + self.getEqualList(s1[1:], s2, memoization), ord(s2[0]) + self.getEqualList(s1, s2[1:], memoization))

        memoization[s1][s2] = sum_value

        return memoization[s1][s2]
```

Method 4 (DFS + Memoization) :
```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        len_s1 = len(s1) + 1
        len_s2 = len(s2) + 1
        memoization: List[List[int]] = [[0]*len_s2 for _ in range(len_s1)]
        return self.getEqualList(s1, s2, 0, 0, memoization)

    def getEqualList(self, s1: str, s2: str, index_s1: int, index_s2: int, memoization: Dict[str, Dict[str, int]]) -> int:
        if memoization[index_s1][index_s2]:
            return memoization[index_s1][index_s2]

        len_s1 = len(s1)
        len_s2 = len(s2)
        if index_s1 > len_s1-1 and index_s2 > len_s2-1:
            return 0
        elif index_s1 > len_s1-1:
            return sum([ord(s2[index]) for index in range(index_s2, len_s2)])
        elif index_s2 > len_s2-1:
            return sum([ord(s1[index]) for index in range(index_s1, len_s1)])

        if s1[index_s1] == s2[index_s2]:
            sum_value = self.getEqualList(s1, s2, index_s1+1, index_s2+1, memoization)
        else:
            sum_value = min(ord(s1[index_s1]) + self.getEqualList(s1, s2, index_s1+1, index_s2, memoization), ord(s2[index_s2]) + self.getEqualList(s1, s2, index_s1, index_s2+1, memoization))

        memoization[index_s1][index_s2] = sum_value

        return memoization[index_s1][index_s2]
```

Method 5 (Dynamic Programming, Bottom Up) :
```python
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        len_s1 = len(s1) + 1
        len_s2 = len(s2) + 1
        memoization = [[0]*len_s2 for _ in range(len_s1)]
        # find ASCII sum of LCS
        lcs = self.findLCS(s1, s2, memoization)

        # Calculate the difference between ASCII sum of s1 and s2 and twice the ASCII sum of LCS
        return sum([ord(char) for char in s1+s2]) - lcs*2

    def findLCS(self, s1: str, s2: str, memoization: List[List[int]]) -> int:
        len_s1 = len(s1)
        len_s2 = len(s2)

        for index_s1 in range(len_s1):
            for index_s2 in range(len_s2):
                if s1[index_s1] == s2[index_s2]:
                    lcs = memoization[index_s1][index_s2] + ord(s1[index_s1])
                else:
                    lcs = max(memoization[index_s1][index_s2+1], memoization[index_s1+1][index_s2])

                memoization[index_s1+1][index_s2+1] = lcs

        return memoization[-1][-1]
```
