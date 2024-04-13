![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 221. [Maximal Square](https://leetcode.com/problems/maximal-square)

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```rust
const ZERO: char = '0';
impl Solution {
    pub fn maximal_square(matrix: Vec<Vec<char>>) -> i32 {
        let mut result: i32 = 0;
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut dp: Vec<i32> = vec![0; n+1];
        for index_m in 0..m {
            let mut dp_temp: Vec<i32> = vec![0; n+1];
            for index_n in 1..n+1 {
                if matrix[index_m][index_n-1] == ZERO {
                    continue
                }

                dp_temp[index_n] = 1 + dp_temp[index_n-1].min(dp[index_n].min(dp[index_n-1]));
                result = result.max(dp_temp[index_n].pow(2));
            }

            dp = dp_temp;
        }

        return result
    }
}
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```rust
const ONE: char = '1';
const ZERO: char = '0';
impl Solution {
    pub fn maximal_square(matrix: Vec<Vec<char>>) -> i32 {
        let mut result: i32 = 0;
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut dp: Vec<i32> = vec![0; n+1];
        for index_m in 0..m {
            let mut previous: i32 = 0;
            for index_n in 0..n {
                let temp: i32 = dp[index_n+1];

                match matrix[index_m][index_n] {
                    ONE => {
                        dp[index_n+1] = 1 + previous.min(dp[index_n].min(dp[index_n+1]));

                        result = result.max(dp[index_n+1].pow(2));
                    },
                    ZERO => dp[index_n+1] = 0,
                    _ => {},
                }

                previous = temp;
            }
        }

        return result
    }
}
```

Method 3 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```rust
const ONE: char = '1';
impl Solution {
    pub fn maximal_square(matrix: Vec<Vec<char>>) -> i32 {
        let mut result: i32 = 0;
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut dp: Vec<i32> = vec![0; n+1];
        for index_m in 0..m {
            let mut previous: i32 = 0;
            for index_n in 0..n {
                let temp: i32 = dp[index_n+1];

                match matrix[index_m][index_n] {
                    ONE => {
                        dp[index_n+1] = 1 + previous.min(dp[index_n].min(dp[index_n+1]));

                        result = result.max(dp[index_n+1].pow(2));
                    },
                    _ => dp[index_n+1] = 0,
                }

                previous = temp;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Dynamic Programming (2-D), Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        dp = [[0] * (n+1) for _ in range(m+1)]
        maximum_length = 0
        for index_m in range(m):
            for index_n in range(n):
                if matrix[index_m][index_n] == "0":
                    continue

                dp[index_m+1][index_n+1] = 1 + min(dp[index_m][index_n], dp[index_m+1][index_n], dp[index_m][index_n+1])
                maximum_length = max(maximum_length, dp[index_m+1][index_n+1])

        return maximum_length ** 2
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        m = len(matrix)
        n = len(matrix[0])
        dp = [0] * (n+1)
        maximum_length = 0
        for index_m in range(m):
            dp_temp = [0] * (n+1)
            for index_n in range(n):
                if matrix[index_m][index_n] == "0":
                    continue

                dp_temp[index_n+1] = 1 + min(dp_temp[index_n], dp[index_n], dp[index_n+1])
                maximum_length = max(maximum_length, dp_temp[index_n+1])

            dp = dp_temp

        return maximum_length ** 2
```

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```go
const ZERO byte = '0'
func maximalSquare(matrix [][]byte) int {
    var result int
    m := len(matrix)
    n := len(matrix[0])
    dp := make([]int, n+1)
    for index_m := 0; index_m < m; index_m++ {
        dp_temp := make([]int, n+1)
        for index_n := 1; index_n < n+1; index_n++ {
            if matrix[index_m][index_n-1] == ZERO {
                continue
            }

            dp_temp[index_n] = 1 + min(dp_temp[index_n-1], dp[index_n-1], dp[index_n])

            result = max(result, dp_temp[index_n] * dp_temp[index_n])
        }

        dp = dp_temp
    }

    return result
}
```
