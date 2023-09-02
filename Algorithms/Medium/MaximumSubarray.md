![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 53. [Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 200/210) :
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        self.result = float('-inf')

        self.dfs(float('-inf'), 0, nums)
        return self.result

    def dfs(self, largest: int, index: int, nums: List[int]):
        self.result = max(self.result, largest)

        if index >= len(nums):
            return None

        # when hasn't choosed any num, we can choose to skip current
        if largest == float('-inf'):
            self.dfs(largest, index+1, nums)

        self.dfs(nums[index]+(0 if largest == float('-inf') else largest), index+1, nums)
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        memoization = defaultdict(lambda: float('-inf'))

        return self.dfs(0, False, memoization, nums)

    def dfs(self, index: int, previous_choosed: bool, memoization: Dict[int, int], nums: List[int]):
        if index >= len(nums):
            return 0 if previous_choosed else float('-inf')

        key = f'{previous_choosed}-{index}'
        if key in memoization:
            return memoization[key]

        choose = nums[index] + self.dfs(index+1, True, memoization, nums)
        # drop all of remaining or choose current
        if previous_choosed:
            result = max(0, choose)
        # when hasn't choosed any num, we can choose to skip current
        else:
            result = max(choose, self.dfs(index+1, False, memoization, nums))

        memoization[key] = result

        return result
```

Method 3 (Dynamic Programming) :
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [float('-inf')] * n
        dp[0] = nums[0]
        for index in range(1, n):
            dp[index] = max(nums[index], dp[index-1]+nums[index])

        return max(dp)
```

Method 4 (Dynamic Programming) :
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        previous = result = nums[0]
        for index in range(1, len(nums)):
            previous = max(previous+nums[index], nums[index])
            result = max(result, previous)

        return result
```

### Solution :

Method 1 (DFS + Memoization) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function maxSubArray($nums) {
        $memoization = [];
        return $this->dfs(0, false, $memoization, $nums);
    }

    function dfs(int $index, bool $hasChoosed, array &$memoization, array &$nums) : int {
        $n = count($nums);
        if ($index >= $n) {
            return $hasChoosed
                ? 0
                : -1000000000000;
        }

        $key = sprintf("%d-%d", $index, $hasChoosed);
        if (isset($memoization[$key])) {
            return $memoization[$key];
        }

        $choose = $nums[$index] + $this->dfs($index+1, true, $memoization, $nums);
        if ($hasChoosed) {
            $result = max(0, $choose);
        } else {
            $result = max($choose, $this->dfs($index+1, false, $memoization, $nums));
        }

        return $memoization[$key] = $result;
    }
}
```

Method 2 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function maxSubArray($nums) {
        $dp = [$nums[0]];
        for ($index = 1; $index < count($nums); $index++) {
            $dp[$index] = max($nums[$index], $nums[$index]+$dp[$index-1]);
        }

        return max($dp);
    }
}
```
