![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2845. [Count Of Interesting Subarrays](https://leetcode.com/problems/count-of-interesting-subarrays)

### Solution :

Method 1 (DFS + Memoization, ERROR: "Memory Limit Exceeded", 609/617) :
```python
class Solution:
    def countInterestingSubarrays(self, nums: List[int], modulo: int, k: int) -> int:
        n = len(nums)
        mapping = [0] * n
        for index, num in enumerate(nums):
            if num % modulo == k:
                mapping[index] = 1

        memoization = [[-1]*n for _ in range(n)]

        self.dfs(0, n-1, memoization, mapping, modulo, k)

        result = 0
        for row in memoization:
            result += sum([value if value > 0 else 0 for value in row])

        return result

    def dfs(self, left: int, right: int, memoization, mapping, modulo, k) -> int:
        if left > right:
            return 0

        if memoization[left][right] != -1:
            return memoization[left][right]

        result = 1 if sum(mapping[left:right+1])%modulo == k else 0
        memoization[left][right] = result

        self.dfs(left+1, right, memoization, mapping, modulo, k)
        self.dfs(left, right-1, memoization, mapping, modulo, k)
        return result
```

Method 2 (ERROR: "Time Limit Exceeded", 609/617) :
```python
class Solution:
    def countInterestingSubarrays(self, nums: List[int], modulo: int, k: int) -> int:
        n = len(nums)
        mapping = [0] * n
        for index, num in enumerate(nums):
            if num % modulo == k:
                mapping[index] = 1

        result = 0
        for index_left in range(n):
            for index_right in range(index_left, n):
                if sum(mapping[index_left:index_right+1])%modulo == k:
                   result += 1

        return result
```

Method 3 (Prefix Sum, Space Complexity: $O(N+K)$ (N: amount of items in array `nums`, K: value of parameter `k`)) :
```python
class Solution:
    def countInterestingSubarrays(self, nums: List[int], modulo: int, k: int) -> int:
        n = len(nums)
        prefix_sum = [0] * n
        prefix_sum[0] = 1 if nums[0] % modulo == k else 0
        for index in range(1, n):
            # Option 1
            prefix_sum[index] = prefix_sum[index-1]
            if nums[index] % modulo == k:
                prefix_sum[index] += 1
            """
            # Option 2

            prefix_sum[index] = prefix_sum[index-1] + (nums[index] % modulo == k)
            """

        result = 0
        mapping = defaultdict(int)
        # Option 1
        mapping[0] = 1
        for prefix in prefix_sum:
            result += mapping[(prefix-k)%modulo]
            mapping[prefix%modulo] += 1
        """
        # Option 2

        for amount in prefix_sum:
            remainder = amount % modulo
            result += (remainder == k)
            key = remainder if k == 0 else (remainder-k)%modulo
            result += mapping[key]
            mapping[remainder] += 1
        """

        return result
```

Method 4 (Prefix Sum, Space Complexity: $O(K)$ (K: value of parameter `k`)) :
```python
class Solution:
    def countInterestingSubarrays(self, nums: List[int], modulo: int, k: int) -> int:
        n = len(nums)
        prefix_sum = 0
        result = 0
        mapping = defaultdict(int)
        for num in nums:
            prefix_sum += num % modulo == k
            remainder = prefix_sum % modulo
            result += (remainder == k)
            key = remainder if k == 0 else (remainder-k)%modulo
            result += mapping[key]
            mapping[remainder] += 1

        return result
```
