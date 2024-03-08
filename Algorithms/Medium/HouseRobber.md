![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 198. [House Robber](https://leetcode.com/problems/house-robber)

### Solution :

Method 1 (DFS) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn rob(nums: Vec<i32>) -> i32 {
        let mut memoization: HashMap<(usize, bool), i32> = HashMap::new();

        return Self::dfs(false, 0, &mut memoization, &nums)
    }

    fn dfs(choosed_previous: bool, index: usize, memoization: &mut HashMap<(usize, bool), i32>, nums: &Vec<i32>) -> i32 {
        let key: (usize, bool) = (index, choosed_previous);
        if memoization.contains_key(&key) {
            return memoization[&key]
        }

        if index >= nums.len() {
            return 0
        }

        let mut result: i32 = Self::dfs(false, index+1, memoization, nums);
        if choosed_previous == false {
            result = result.max(nums[index] + Self::dfs(true, index+1, memoization, nums));
        }

        /* Option 1 */
        memoization.entry(key).or_insert(result);
        /* Option 2

        memoization.insert(key, result);
        */

        return result
    }
}
```

Method 2 (Dynamic Programming) :
```rust
impl Solution {
    pub fn rob(nums: Vec<i32>) -> i32 {
        let mut dp: (i32, i32) = (0, 0);
        for num in nums {
            dp = (dp.1, dp.1.max(num+dp.0));
        }

        return dp.0.max(dp.1)
    }
}
```

### Solution :

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        memoization = {}
        self.dfs(False, 0, memoization, nums)

        return max(memoization.values())

    def dfs(self, choosed_previous: bool, index: int, memoization: Dict[Tuple[int, bool], int], nums: List[int]) -> int:
        key = (index, choosed_previous)
        if key in memoization:
            return memoization[key]

        if index >= len(nums):
            return 0

        result = self.dfs(False, index+1, memoization, nums)
        if not choosed_previous:
            result = max(result, nums[index] + self.dfs(True, index+1, memoization, nums))

        memoization[key] = result
        return result
```

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [{} for _ in range(n)]
        dp[0] = {False: 0, True: nums[0]}
        for index in range(1, n):
            dp[index] = {
                False: max(dp[index-1].values()),
                True: nums[index] + dp[index-1][False],
            }

        return max([max(items.values()) for items in dp])
```

Method 3 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        # Option 1
        dp = {False: 0, True: nums[0]}
        for index in range(1, n):
            dp = {
                False: max(dp.values()),
                True: nums[index] + dp[False],
            }

        return max(dp.values())
        """
        # Option 2

        dp = [0, nums[0]]
        for index in range(1, n):
            dp = [max(dp), nums[index] + dp[0]]

        return max(dp)
        """
        """
        # Option 3

        rob_non_previous, rob_with_previous = 0, 0 
        for num in nums:
            rob_non_previous, rob_with_previous = rob_with_previous, max(num + rob_non_previous, rob_with_previous)

        return rob_with_previous
        """
```
