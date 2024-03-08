![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1658. [Minimum Operations To Reduce X To Zero](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero)

### Solution :

Method 1 (DFS, Time Complexity: $O(2^N)$, ERROR: "Time Limit Exceeded", 10/94) :
```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        self.result = float('inf')
        self.dfs(0, len(nums)-1, x, nums)
        return -1 if self.result == float('inf') else self.result

    def dfs(self, left, right, x, nums):
        n = len(nums)
        if x == 0:
            self.result = min(self.result, left + ((n-1)-right))
            return None

        if left >= n or right < 0 or left > right:
            return None
        if x < 0:
            return None

        self.dfs(left+1, right, x-nums[left], nums)
        self.dfs(left, right-1, x-nums[right], nums)
```

Method 2 (DFS + Memoization, Time Complexity: $O(N^2)$, ERROR: "Memory Limit Exceeded", 73/94) :
```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        visited = set()
        self.result = float('inf')
        self.dfs(0, len(nums)-1, x, visited, nums)
        return -1 if self.result == float('inf') else self.result

    def dfs(self, left, right, x, visited, nums):
        key = (left, right)
        if key in visited:
            return None

        n = len(nums)
        if x == 0:
            self.result = min(self.result, left + ((n-1)-right))
            return None

        if left >= n or right < 0 or left > right:
            return None
        if x < 0:
            return None

        self.dfs(left+1, right, x-nums[left], visited, nums)
        self.dfs(left, right-1, x-nums[right], visited, nums)

        visited.add(key)
```

Method 3 ([Two Pointer](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/?envType=daily-question&envId=2023-09-20), Time Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        # Option 1
        n = len(nums)
        sum_target = sum(nums) - x
        if sum_target == 0:
            return n

        sum_current = 0
        maximum = 0
        left = 0
        for right in range(n):
            sum_current += nums[right]
            while left <= right and sum_current > sum_target:
                sum_current -= nums[left]
                left += 1

            if sum_current == sum_target:
                maximum = max(maximum, right-left+1)

        return -1 if maximum == 0 else n - maximum
        """
        # Option 2

        n = len(nums)
        sum_target = sum(nums) - x
        sum_current = 0
        maximum = -1
        left = 0
        for right in range(n):
            sum_current += nums[right]
            while left <= right and sum_current > sum_target:
                sum_current -= nums[left]
                left += 1

            if sum_current == sum_target:
                maximum = max(maximum, right-left+1)

        return -1 if maximum == -1 else n - maximum
        """
```

Method 4 (Prefix Sum, Time Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        n = len(nums)
        sum_remain = sum(nums) - x
        sum_current = 0
        maximum = -1

        # Option 1
        prefix_sum = {}
        for right in range(n):
            sum_current += nums[right]
            prefix_sum[sum_current] = right

            if sum_current == sum_remain:
                maximum = max(maximum, right+1)
            elif sum_current > sum_remain and sum_current-sum_remain in prefix_sum:
                maximum = max(maximum, right-prefix_sum[sum_current-sum_remain])
        """
        # Option 2

        prefix_sum = {0: -1}
        for right in range(n):
            sum_current += nums[right]
            prefix_sum[sum_current] = right
            sum_remove = sum_current - sum_remain
            if sum_remove in prefix_sum:
                maximum = max(maximum, right-prefix_sum[sum_remove])
        """

        return -1 if maximum == -1 else n-maximum
```

### Solution :

Method 1 (Two Pointer) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $x
     * @return Integer
     */
    function minOperations($nums, $x) {
        $n = count($nums);
        $sumRemaining = array_sum($nums) - $x;
        $sumCurrent = 0;
        $maximum = -1;
        $left = 0;
        for ($right = 0; $right < $n; $right++) {
            $sumCurrent += $nums[$right];
            while ($left <= $right && $sumCurrent > $sumRemaining) {
                $sumCurrent -= $nums[$left++];
            }

            if ($sumCurrent == $sumRemaining) {
                $maximum = max($maximum, $right-$left+1);
            }
        }

        return $maximum == -1
            ? -1
            : $n - $maximum;
    }
}
```

Method 2 (Prefix Sum) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $x
     * @return Integer
     */
    function minOperations($nums, $x) {
        $n = count($nums);
        $prefixSum = [0 => -1];
        $sumRemain = array_sum($nums) - $x;
        $sumCurrent = 0;
        $maximum = -1;
        for ($index = 0; $index < $n; $index++) {
            $sumCurrent += $nums[$index];
            $prefixSum[$sumCurrent] = $index;

            $sumRemove = $sumCurrent - $sumRemain;
            if (isset($prefixSum[$sumRemove])) {
                $maximum = max($maximum, $index - $prefixSum[$sumRemove]);
            }
        }

        return $maximum == -1
            ? -1
            : $n - $maximum;
    }
}
```
