![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2707. [Extra Characters In A String](https://leetcode.com/problems/extra-characters-in-a-string)

### Solution :

Method 1 (DFS, Time Complexity: $O(M+N^2)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `dictionary`, N: the length of `s`, K: the average length of the strings in `dictionary`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn min_extra_char(s: String, dictionary: Vec<String>) -> i32 {
        let n: usize = s.len();
        let mut set: HashSet<&String> = HashSet::from_iter(dictionary.iter());
        let mut memoization: Vec<i32> = vec![-1; n];

        return Self::dfs(0, &mut memoization, &set, &s)
    }

    fn dfs(index: usize, memoization: &mut Vec<i32>, set: &HashSet<&String>, s: &String) -> i32 {
        let n: usize = s.len();
        if index >= n {
            return 0
        }
        if memoization[index] >= 0 {
            return memoization[index]
        }

        let mut result: i32 = 1 + Self::dfs(index+1, memoization, set, s);;
        for index_next in index..n {
            let substring: String = s[index..=index_next].to_string();
            if set.contains(&&substring) {
                result = i32::min(result, Self::dfs(index_next+1, memoization, set, s));
            }
        }

        memoization[index] = result;
        return result
    }
}
```

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def minExtraChar(self, s: str, dictionary: List[str]) -> int:
        self.result = float('inf')
        self.dfs(0, 0, s, set(dictionary))
        return self.result

    def dfs(self, index: int, amount_unused: int, s: str, dictionary: Set[str]):
        len_s = len(s)
        if amount_unused >= self.result:
            return None

        if index >= len_s:
            self.result = min(self.result, amount_unused)
            return None

        self.dfs(index+1, amount_unused+1, s, dictionary)
        for index_substring in range(index, len_s):
            if s[index:index_substring+1] not in dictionary:
                continue

            self.dfs(index_substring+1, amount_unused, s, dictionary)
```

Method 2 (Dynamic Programming, Time Complexity: $O(N^3)$) :
```python
class Solution:
    def minExtraChar(self, s: str, dictionary: List[str]) -> int:
        n = len(s) + 1
        dictionary = set(dictionary)
        dp = [float('inf')] * (n)
        dp[0] = 0
        for index_end in range(1, n):
            # use the minimum extra amount at previous position as default extra amount of current position
            dp[index_end] = dp[index_end-1] + 1
            for index_start in range(index_end+1):
                if s[index_start:index_end] not in dictionary:
                    continue

                dp[index_end] = min(dp[index_end], dp[index_start])

        return dp[-1]
```

### Solution :

Method 1 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param String $s
     * @param String[] $dictionary
     * @return Integer
     */
    function minExtraChar($s, $dictionary) {
        $n = strlen($s) + 1;
        $dp = array_fill(0, $n, INF);
        $dp[0] = 0;
        for ($amountS = 1; $amountS < $n; $amountS++) {
            $dp[$amountS] = $dp[$amountS-1] + 1;
            for ($offset = 1; $offset < $amountS+1; $offset++) {
                $indexStart = $amountS - $offset;
                if (!in_array(
                    substr($s, $indexStart, $offset),
                    array_values($dictionary)
                )) {
                    continue;
                }

                $dp[$amountS] = min($dp[$amountS], $dp[$indexStart]);
            }
        }

        return $dp[$n-1];
    }
}
```
