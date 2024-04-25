![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2370. [Longest Ideal Subsequence](https://leetcode.com/problems/longest-ideal-subsequence)

### Solution :

Method 1 (Dynamic Programming + Space Optimization + Built-In Method, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn longest_ideal_string(s: String, k: i32) -> i32 {
        let k: usize = k as usize;
        let mut dp: [i32; 26] = [0; 26];
        for byte in s.bytes().into_iter() {
            let index: usize = (byte - BASE) as usize;
            /* Option 1 */
            let mut index_start: usize = index - k;
            if index_start > 25 {
                index_start = 0;
            }
            /* Option 2

            let mut index_start: usize = match index >= k {
                true => index - k,
                false => 0
            };
            */
            for index_previous in index_start..=(index+k).min(25) {
                if dp[index] >= dp[index_previous] {
                    continue;
                }

                dp[index] = dp[index_previous];
            }

            dp[index] += 1;
        }
        return dp.into_iter().max().unwrap()
    }
}
```

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [[0]*26 for _ in range(26)]
        for char in s:
            current = ord(char) - BASE
            dp[current][current] = 1 + max(dp[current])
            for offset in range(1, k+1):
                index_previous = current - offset
                if index_previous >= 0:
                    dp[current][index_previous] = 1 + max(dp[index_previous])

                index_next = current + offset
                if index_next < 26:
                    dp[current][index_next] = 1 + max(dp[index_next])

        return max(max(row) for row in dp)
```

Method 2 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [[0]*(k*2 + 1) for _ in range(26)]
        for char in s:
            current = ord(char) - BASE
            dp[current][0] = 1 + max(dp[current])
            for offset in range(-k, k+1):
                if offset == 0:
                    continue

                index_previous = current + offset
                if 0 <= index_previous < 26:
                    dp[current][offset] = 1 + max(dp[index_previous])

        return max(max(row) for row in dp)
```

Method 3 (Dynamic Programming + Space Optimization, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [0] * 26
        for char in s:
            current = ord(char) - BASE
            temp = 0
            # Option 1
            for offset in range(-k, k+1):
                index_previous = current + offset
            """
            # Option 2

            for index_previous in range(current-k, current+k+1):
            """
                if 0 <= index_previous < 26:
                    temp = max(temp, dp[index_previous])
            dp[current] = 1 + temp

        return max(dp)
```

Method 4 (Dynamic Programming + Space Optimization + Built-In Method, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [0] * 26
        for char in s:
            current = ord(char) - BASE
            # Option 1
            dp[current] = 1 + max(dp[max(0, current-k):min(26, current+k+1)])
            """
            # Option 2

            for index_previous in range(current-k, current+k+1):
                if 0 <= index_previous < 26 and dp[index_previous] > dp[current]:
                    dp[current] = dp[index_previous]
            dp[current] += 1
            """

        return max(dp)
```

### Solution :

Method 1 (Dynamic Programming + Space Optimization + Built-In Method, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```go
const BASE int = int('a')
func longestIdealString(s string, k int) int {
    var dp [26]int
    var result int
    for _, char := range s {
        index := int(char) - BASE
        for index_next := max(0, index-k); index_next < min(26, index+k+1); index_next++ {
            if dp[index_next] > dp[index] {
                dp[index] = dp[index_next]
            }
        }

        dp[index]++
        if dp[index] > result {
            result = dp[index]
        }
    }

    return result
}
```
