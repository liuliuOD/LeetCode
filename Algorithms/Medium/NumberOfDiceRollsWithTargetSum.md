![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1155. [Number Of Dice Rolls With Target Sum](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;

const MODULAR: i64 = 1_000_000_007;
impl Solution {
    pub fn num_rolls_to_target(n: i32, k: i32, target: i32) -> i32 {
        let k: i64 = k as i64;
        let target: i64 = target as i64;
        let mut memoization: HashMap<(i32, i64), i64> = HashMap::new();

        return Self::dfs(n, target, &mut memoization, k) as i32
    }

    fn dfs(n_remaining: i32, target: i64, memoization: &mut HashMap<(i32, i64), i64>, k: i64) -> i64 {
        if n_remaining == 0 && target == 0 {
            return 1
        }
        if n_remaining <= 0 || target <= 0 {
            return 0
        }

        let key: (i32, i64) = (n_remaining, target);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: i64 = 0;
        for value in 1..=k {
            result = (result + Self::dfs(n_remaining-1, target-value, memoization, k)) % MODULAR;
        }

        memoization.entry(key).or_insert(result);
        return result
    }
}
```

### Solution :

Method 1 (DFS, Time Complexity: $O(M*N*K)$ (M: amount of `target`, N: amount of `n`, K: amount of `k`), Space Complexity: $O(M*N)$ (M: amount of `target`, N: amount of `n`)) :
```python
MODULAR = 1_000_000_007

class Solution:
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        memoization = defaultdict(int)

        return self.dfs(n, target, memoization, k)

    def dfs(self, n_remaining: int, target: int, memoization: Dict[Tuple[int, int], int], k: int) -> int:
        if n_remaining == 0 and target == 0:
            return 1

        if n_remaining <= 0 or target <= 0:
            return 0

        key = (n_remaining, target)
        if key in memoization:
            return memoization[key]

        result = 0
        for value in range(1, k+1):
            result = (result + self.dfs(n_remaining-1, target-value, memoization, k)) % MODULAR

        memoization[key] = result
        return result
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N*K)$ (M: amount of `target`, N: amount of `n`, K: amount of `k`), Space Complexity: $O(M)$ (M: amount of `target`)) :
```python
MODULAR = 1_000_000_007

class Solution:
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        dp = defaultdict(int)
        for value in range(1, k+1):
            dp[value] = 1

        for n_current in range(2, n+1):
            temp = defaultdict(int)
            for value_previous in dp.keys():
                for value_current in range(1, k+1):
                    value_sum = value_previous + value_current
                    temp[value_sum] = (temp[value_sum] + dp[value_previous]) % MODULAR

            dp = temp

        return dp[target]
```
