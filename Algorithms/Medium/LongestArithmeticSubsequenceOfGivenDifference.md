![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1218. [Longest Arithmetic Subsequence Of Given Difference](https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference)

### [Solution](https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/solutions/3761630/python3-intuition-clear-code-explanations) :

Method 1 (DP, ERROR: "Time Limit Exceeded", 34/39) :
```python
class Solution:
    def longestSubsequence(self, arr: List[int], difference: int) -> int:
        n = len(arr)
        memoization = [1] * n
        result = 1
        for index, value in enumerate(arr):
            for index_previous in range(index):
                if  arr[index] - arr[index_previous] != difference:
                    continue
                
                if memoization[index_previous] >= memoization[index]:
                    memoization[index] = memoization[index_previous] + 1
                    result = max(result, memoization[index])
        
        return result
```

Method 2 (DP) :
```python
class Solution:
    def longestSubsequence(self, arr: List[int], difference: int) -> int:
        memoization = defaultdict(int)
        for value in arr:
            value_previous = value - difference
            if value_previous in memoization:
                memoization[value] = 1 + memoization[value_previous]
            else:
                memoization[value] = 1

        return max(memoization.values())
```
