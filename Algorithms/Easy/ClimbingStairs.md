![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## [Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn climb_stairs(n: i32) -> i32 {
        match n {
            0 | 1 => 1,
            value => Self::climb_stairs(n - 1) + Self::climb_stairs(n - 2),
        }
    }
}
```

Method 2 (Dynamic Programming, Top to Bottom) :
```rust
use std::collections::HashMap;
impl Solution {

    pub fn climb_stairs(n: i32) -> i32 {
        let mut hm = HashMap::from([(0, 1), (1, 1)]);

        Self::dynamic_programming(n, &mut hm)
    }

    fn dynamic_programming(n: i32, hm: &mut HashMap<i32, i32>) -> i32 {
        match hm.get(&n) {
            Some(&value) => value,
            None => {
                let sum = Self::dynamic_programming(n - 1, hm) + Self::dynamic_programming(n - 2, hm);
                hm.insert(n, sum);

                return *hm.get(&n).unwrap()
            },
        }
    }
}
```

Method 3 (Bottom to Top) :
```rust
impl Solution {

    pub fn climb_stairs(n: i32) -> i32 {
        let mut start = [(0, 1), (1, 1)];
        while start[1].0 < n {
            let sum = start[0].1 + start[1].1;
            start[0] = (start[0].0 + 1, start[1].1);
            start[1] = (start[1].0 + 1, sum);
        }
        start[1].1
    }
}
```

Method 4 :
```rust
impl Solution {

    pub fn climb_stairs(n: i32) -> i32 {
        let mut dp_1: i32 = 1;
        let mut dp_2: i32 = 1;
        for _ in 2..=n {
            let temp: i32 = dp_1 + dp_2;
            dp_1 = dp_2;
            dp_2 = temp;
        }

        return dp_2
    }
}
```

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        dp = [1, 1]
        for current in range(2, n+1):
            dp.append(dp[current-1] + dp[current-2])

        return dp[-1]
```

Method 2 (Dynamic Programming + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        dp_1 = 1
        dp_2 = 1
        for _ in range(2, n+1):
            temp = dp_1 + dp_2
            dp_1, dp_2 = dp_2, temp

        return dp_2
```
