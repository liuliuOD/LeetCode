![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 974. [Subarray Sums Divisible By K](https://leetcode.com/problems/subarray-sums-divisible-by-k)

### Solution :

Method 1 (Prefix Sum, ERROR: "Time Limit Exceeded", 66/73) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = [0] * n
        prefix_sum[0] = nums[0]
        for index in range(1, n):
            prefix_sum[index] = prefix_sum[index-1] + nums[index]

        result = 0
        for index_left in range(n):
            for index_right in range(index_left, n):
                redundant = prefix_sum[index_left-1] if index_left > 0 else 0
                if (prefix_sum[index_right] - redundant) % k == 0:
                    result += 1

        return result
```

Method 2 (Prefix Sum + Hash Map, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = [0] * n
        prefix_sum[0] = nums[0]
        for index in range(1, n):
            prefix_sum[index] = nums[index] + prefix_sum[index-1]

        mapping = defaultdict(int)
        result = 0
        for index in range(n):
            """
            if x % k = n and y % k = n, then (x-y) % k = 0.
            because x = a*k + n and y = b*k + n,
            x - y = k*(a - b) + (n - n) = k*(a - b)
            """
            remainder = prefix_sum[index] % k
            # Option 1
            result += mapping[remainder] + (remainder == 0)
            """
            # Option 2

            result += remainder == 0
            result += mapping[remainder]
            """

            mapping[remainder] += 1
        return result
```

Method 3 (Prefix Sum + Hash Map, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = 0
        mapping = defaultdict(int)
        result = 0
        for index in range(n):
            prefix_sum += nums[index]
            remainder = prefix_sum % k
            result += mapping[remainder] + (remainder == 0)
            mapping[remainder] += 1

        return result
```
