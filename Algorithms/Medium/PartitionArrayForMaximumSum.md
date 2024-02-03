![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1043. [Partition Array For Maximum Sum](https://leetcode.com/problems/partition-array-for-maximum-sum)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N*K)$ (N: length of `arr`, K: value of `k`), Space Complexity: $O(N*K)$) :
```python
class Solution:
    def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, 1, memoization, arr, k)

    def dfs(self, index: int, amount: int, memoization: Dict, arr: List[int], k: int) -> int:
        n = len(arr)
        if index+amount-1 == n-1:
            return max(arr[index:index+amount]) * amount if amount and index < n else 0

        key = (index, amount)
        if key in memoization:
            return memoization[key]

        result = max(arr[index:index+amount])*amount + self.dfs(index+amount, 1, memoization, arr, k)
        if amount < k:
            result = max(result, self.dfs(index, amount+1, memoization, arr, k))

        memoization[key] = result
        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(N*K)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, memoization, arr, k)

    def dfs(self, index: int, memoization: Dict, arr: List[int], k: int) -> int:
        if index in memoization:
            return memoization[index]

        result = 0
        for amount in range(1, k+1):
            if index+amount > len(arr):
                break

            result = max(result, max(arr[index:index+amount])*amount + self.dfs(index+amount, memoization, arr, k))

        memoization[index] = result
        return result
```
