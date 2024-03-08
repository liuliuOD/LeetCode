![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 55. [Jump Game](https://leetcode.com/problems/jump-game)

### Solution :

Method 1 (DFS + Memoization + Pruning) :
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        memoization = defaultdict(bool)
        return self.dfs(0, memoization, nums)

    def dfs(self, index: int, memoization: Dict[int, bool], nums: List[int]) -> bool:
        if index >= len(nums)-1:
            return True

        result = False
        for index_next in range(index+1, index+nums[index]+1):
            if result:
                break

            if index_next in memoization:
                result |= memoization[index_next]
                continue

            result_next = self.dfs(index_next, memoization, nums)
            memoization[index_next] = result_next
            result |= result_next

        memoization[index] = result

        return result
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        dp = [False] * n
        dp[0] = True
        for index in range(1, n):
            # reverse range order to prune extra calculation
            for index_previous in reversed(range(index)):
                if dp[index_previous] and index_previous+nums[index_previous] >= index:
                    dp[index] = True
                    break

        return dp[-1]
```

Method 3 (Kadane's Algorithm) :
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        jump_maximum = 0
        for index, num in enumerate(nums):
            if jump_maximum < index:
                return False

            jump_maximum = max(jump_maximum, index+num)

        return True
```

### Solution :

Method 1 (Kadane's Algorithm) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function canJump($nums) {
        $maximum = 0;
        foreach($nums as $index => $num) {
            if ($maximum < $index) {
                return false;
            }

            $maximum = max($maximum, $index+$nums[$index]);
        }

        return true;
    }
}
```

Method 2 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function canJump($nums) {
        $n = count($nums);
        $dp = array_fill(0, $n, false);
        $dp[0] = true;
        for ($index = 1; $index < $n; $index++) {
            for ($indexPrevious = $index-1; $indexPrevious >= 0; $indexPrevious--) {
                if ($dp[$indexPrevious] && $indexPrevious+$nums[$indexPrevious] >= $index) {
                    $dp[$index] = true;
                    break;
                }
            }
        }

        return $dp[$n-1];
    }
}
```
