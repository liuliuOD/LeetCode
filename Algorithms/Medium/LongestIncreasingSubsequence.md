![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 300. [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence)

### Solution :

Method 1 (DFS + Memoization) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn length_of_lis(nums: Vec<i32>) -> i32 {
        let mut memoization: HashMap<usize, i32> = HashMap::new();
        return Self::dfs(-10_001, 0, &mut memoization, &nums)
    }

    fn dfs(previous: i32, index: usize, memoization: &mut HashMap<usize, i32>, nums: &Vec<i32>) -> i32 {
        let n: usize = nums.len();
        if index >= n {
            return 0
        }

        if memoization.contains_key(&index) {
            return *memoization.get(&index).unwrap()
        }

        let mut result: i32 = 0;
        for index_current in index..n {
            if previous >= nums[index_current] {
                continue;
            }

            result = result.max(1+Self::dfs(nums[index_current], index_current+1, memoization, nums)).max(Self::dfs(previous, index_current+1, memoization, nums));
        }

        memoization.insert(index, result);
        return result
    }
}
```

Method 2 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: difference between maximum and minimum in `nums`, N: length of `nums`), Space Complexity: $O(M)$) :
```rust
impl Solution {
    pub fn length_of_lis(nums: Vec<i32>) -> i32 {
        let minimum: i32 = *nums.iter().min().unwrap();
        let maximum: i32 = *nums.iter().max().unwrap();
        let mut counter: Vec<i32> = vec![0; (maximum - minimum + 1) as usize];
        for num in nums.into_iter() {
            let index: usize = (num - minimum) as usize;
            counter[index] = 1 + counter[..index].to_vec().iter().max().unwrap_or(&0);
        }

        return counter.into_iter().max().unwrap()
    }
}
```

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

Method 3 (Dynamic Programming, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
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

Method 4 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: difference between maximum and minimum in `nums`, N: length of `nums`), Space Complexity: $O(M)$) :
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        minimum = min(nums)
        maximum = max(nums)
        counter = [0] * (maximum - minimum + 1)
        for num in nums:
            index = num - minimum
            counter[index] = 1 + (max(counter[:index]) if index else 0)

        return max(counter)
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

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: difference between maximum and minimum in `nums`, N: length of `nums`), Space Complexity: $O(M)$) :
```go
func lengthOfLIS(nums []int) int {
    minimum := slices.Min(nums)
    maximum := slices.Max(nums)
    dp := make([]int, maximum - minimum + 1)
    for _, num := range nums {
        index := num - minimum
        dp[index] = 1
        if index > 0 {
            dp[index] += slices.Max(dp[:index])
        }
    }

    return slices.Max(dp)
}
```
