![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 935. [Knight Dialer](https://leetcode.com/problems/knight-dialer)

### Solution :

Method 1 :
```rust
const MODULO: i32 = 1_000_000_007;

impl Solution {
    pub fn knight_dialer(n: i32) -> i32 {
        let MAPPING: Vec<Vec<usize>> = vec![
            vec![4, 6],
            vec![6, 8],
            vec![7, 9],
            vec![4, 8],
            vec![0, 3, 9],
            vec![],
            vec![0, 1, 7],
            vec![2, 6],
            vec![1, 3],
            vec![2, 4]
        ];
        let mut dp: Vec<i32> = vec![1; 10];
        for n_current in 1..n {
            let mut dp_temp: Vec<i32> = vec![0; 10];
            for number in 0..=9 {
                for &number_previous in MAPPING[number].iter() {
                    dp_temp[number] = (dp_temp[number] + dp[number_previous]) % MODULO;
                }
            }

            dp = dp_temp;
        }

        return dp.into_iter().reduce(|summation, value| (summation+value)%MODULO).unwrap()
    }
}
```

### Solution :

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
MODULO = 1_000_000_007
MAPPING = [
    [4, 6,],
    [6, 8,],
    [7, 9,],
    [4, 8,],
    [0, 3, 9,],
    [],
    [0, 1, 7,],
    [2, 6,],
    [1, 3,],
    [2, 4,],
]

class Solution:
    def knightDialer(self, n: int) -> int:
        result = 0
        memoization = {}
        for index in range(10):
            result = (result + self.dfs(index, n-1, memoization)) % MODULO

        return result

    def dfs(self, index: int, n: int, memoization: Dict[Tuple[int, int], int]) -> int:
        key = (index, n)
        if key in memoization:
            return memoization[key]

        if n == 0:
            return 1

        result = 0
        for index_next in MAPPING[index]:
            result = (result + self.dfs(index_next, n-1, memoization)) % MODULO

        memoization[key] = result
        return result
```

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
MODULO = 1_000_000_007
MAPPING = [
    [4, 6,],
    [6, 8,],
    [7, 9,],
    [4, 8,],
    [0, 3, 9,],
    [],
    [0, 1, 7,],
    [2, 6,],
    [1, 3,],
    [2, 4,],
]

class Solution:
    def knightDialer(self, n: int) -> int:
        dp: List[List[int]] = [[] for _ in range(n)]
        dp[0] = [1 for _ in range(10)]
        for index in range(1, n):
            for number in range(10):
                temp = 0
                for number_previous in MAPPING[number]:
                    temp = (temp + dp[index-1][number_previous]) % MODULO

                dp[index].append(temp)

        return sum(dp[n-1]) % MODULO
```

Method 3 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
MODULO = 1_000_000_007
MAPPING = [
    [4, 6,],
    [6, 8,],
    [7, 9,],
    [4, 8,],
    [0, 3, 9,],
    [],
    [0, 1, 7,],
    [2, 6,],
    [1, 3,],
    [2, 4,],
]

class Solution:
    def knightDialer(self, n: int) -> int:
        dp: List[int] = [1 for _ in range(10)]
        for index in range(1, n):
            # Option 1
            temp_dp = []
            for number in range(10):
                temp_result = 0
                for number_previous in MAPPING[number]:
                    temp_result = (temp_result + dp[number_previous]) % MODULO

                temp_dp.append(temp_result)
            """
            # Option 2

            temp_dp = [0] * 10
            for number in range(10):
                for number_previous in MAPPING[number]:
                    temp_dp[number] = (temp_dp[number] + dp[number_previous]) % MODULO
            """

            dp = temp_dp

        return sum(dp) % MODULO
```

Method 4 ([Efficient Iteration On States](https://leetcode.com/problems/knight-dialer/editorial), Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
MODULO = 1_000_000_007

class Solution:
    def knightDialer(self, n: int) -> int:
        GROUP_A = 4
        GROUP_B = 2
        GROUP_C = 2
        GROUP_D = 1
        if n == 1:
            return GROUP_A + GROUP_B + GROUP_C + GROUP_D + 1

        for _ in range(n-1):
            GROUP_A, GROUP_B, GROUP_C, GROUP_D = 2*(GROUP_B+GROUP_C)%MODULO, GROUP_A, (GROUP_A+2*GROUP_D)%MODULO, GROUP_C

        return (GROUP_A+GROUP_B+GROUP_C+GROUP_D) % MODULO
```
