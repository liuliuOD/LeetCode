![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 300. [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 22/54) :
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        result = 0
        for index in range(len(nums)):
            result = max(result, 1 + self.dfs(index, nums))

        return result

    def dfs(self, index: int, nums: List[int]) -> int:
        if index >= len(nums):
            return 0

        result = 0
        for index_next in range(index+1, len(nums)):
            if nums[index_next] <= nums[index]:
                continue

            result = max(result, 1 + self.dfs(index_next, nums))

        return result
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        memoization = {}
        result = 0
        for index in range(len(nums)):
            result = max(result, 1 + self.dfs(index, memoization, nums))

        return result

    def dfs(self, index: int, memoization: Dict[int, int], nums: List[int]) -> int:
        if index in memoization:
            return memoization[index]

        if index >= len(nums):
            return 0

        result = 0
        for index_next in range(index+1, len(nums)):
            if nums[index_next] <= nums[index]:
                continue

            result = max(result, 1 + self.dfs(index_next, memoization, nums))

        memoization[index] = result
        return result
```

Method 3 (Dynamic Programming) :
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1] * n
        for index in reversed(range(n)):
            for index_next in range(index+1, n):
                if nums[index_next] <= nums[index]:
                    continue

                dp[index] = max(dp[index], 1 + dp[index_next])

        return max(dp)
```

### Solution :

Method 1 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function lengthOfLIS($nums) {
        $n = count($nums);
        $dp = array_fill(0, $n, 1);
        for ($index = $n-1; $index >= 0; $index--) {
            for ($indexNext = $index+1; $indexNext < $n; $indexNext++) {
                if ($nums[$index] >= $nums[$indexNext]) {
                    continue;
                }

                $dp[$index] = max($dp[$index], 1 + $dp[$indexNext]);
            }
        }

        return max($dp);
    }
}
```
