![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2919. [Minimum Increment Operations To Make Array Beautiful](https://leetcode.com/problems/minimum-increment-operations-to-make-array-beautiful)

### Solution :

Method 1 (DFS + Memoization) :
```rust
use std::cmp::{min, max};

impl Solution {
    pub fn min_increment_operations(nums: Vec<i32>, k: i32) -> i64 {
        let n: usize = nums.len();
        let mut memoization: Vec<i64> = vec![-1; n];
        return Self::dfs(0, &mut memoization, k, &nums)
    }

    fn dfs(index: usize, memoization: &mut Vec<i64>, k: i32, nums: &Vec<i32>) -> i64 {
        let n: usize = nums.len();
        if index < n && memoization[index] >= 0 {
            return memoization[index]
        }

        if index > n-3 {
            return 0
        }

        let temp: i64 = *[
            (0.max(k-nums[index]) as i64) + Self::dfs(index+1, memoization, k, nums),
            (0.max(k-nums[index+1]) as i64) + Self::dfs(index+2, memoization, k, nums),
            (0.max(k-nums[index+2]) as i64) + Self::dfs(index+3, memoization, k, nums),
        ].iter().min().unwrap();
        memoization[index] = temp;
        return temp
    }
}
```

Method 2 (Dynamic Programming) :
```rust
impl Solution {
    pub fn min_increment_operations(nums: Vec<i32>, k: i32) -> i64 {
        let mut dp: Vec<i64> = vec![0.max((k-nums[0]) as i64), 0.max((k-nums[1]) as i64), 0.max((k-nums[2]) as i64)];
        for index in 3..nums.len() {
            let temp: i64 = 0.max((k-nums[index]) as i64) + *dp.iter().min().unwrap();
            dp = vec![dp[1], dp[2], temp];
        }

        return *dp.iter().min().unwrap()
    }
}
```

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        memoization = [-1] * len(nums)
        return self.dfs(0, memoization, k, nums)

    def dfs(self, index: int, memoization: List[int], k: int, nums: List[int]) -> int:
        n = len(nums)
        if index < n and memoization[index] >= 0:
            return memoization[index]

        if index > n-3:
            return 0

        memoization[index] = min(
            max(0, k-nums[index]) + self.dfs(index+1, memoization, k, nums),
            max(0, k-nums[index+1]) + self.dfs(index+2, memoization, k, nums),
            max(0, k-nums[index+2]) + self.dfs(index+3, memoization, k, nums)
        )
        return memoization[index]
```

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [-1] * n
        dp[0], dp[1], dp[2] = max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])
        for index in range(3, n):
            dp[index] = max(0, k-nums[index]) + min(dp[index-1], dp[index-2], dp[index-3])

        return min(dp[-1], dp[-2], dp[-3])
```

Method 3 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        n = len(nums)
        # Option 1
        dp = deque([max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])])
        for index in range(3, n):
            dp.append(max(0, k-nums[index]) + min(dp[0], dp[1], dp[2]))
            dp.popleft()
        """
        # Option 2

        dp = [max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])]
        for index in range(3, n):
            dp[0], dp[1], dp[2] = dp[1], dp[2], max(0, k-nums[index]) + min(dp[0], dp[1], dp[2])
        """

        return min(dp)
```
