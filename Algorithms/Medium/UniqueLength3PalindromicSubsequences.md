![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1930. [Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences)

### Solution :

Method 1 (Hash Map + Set) :
```rust
use std::iter::FromIterator;
use std::collections::HashSet;

impl Solution {
    pub fn count_palindromic_subsequence(s: String) -> i32 {
        let s: Vec<char> = s.chars().into_iter().collect::<Vec<char>>();
        let mut result: i32 = 0;
        for ch in HashSet::<char>::from_iter(s.clone()) {
            let index_left: usize = s.iter().position(|&item| item == ch).unwrap();
            let index_right: usize = s.iter().rposition(|&item| item == ch).unwrap();
            if index_left+1 >= index_right {
                continue;
            }

            result += (HashSet::<&char>::from_iter(&s[index_left+1..index_right])).len() as i32;
        }

        return result
    }
}
```

Method 2 :
```rust
use std::iter::FromIterator;
use std::collections::HashSet;

impl Solution {
    pub fn count_palindromic_subsequence(s: String) -> i32 {
        let mut result: i32 = 0;
        for ch in HashSet::<char>::from_iter(s.chars()) {
            let index_left: usize = s.find(ch).unwrap();
            let index_right: usize = s.rfind(ch).unwrap();
            if index_left+1 >= index_right {
                continue;
            }

            result += HashSet::<char>::from_iter((&s[index_left+1..index_right]).chars()).len() as i32;
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map + Set) :
```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        mapping = defaultdict(list)
        for index, char in enumerate(s):
            mapping[char].append(index)

        result = 0
        visited = defaultdict(set)
        for index, char in enumerate(s):
            if char in visited:
                continue

            index_right = mapping[char][-1]
            for index_center in range(index+1, index_right):
                visited[char].add(char+s[index_center])

            result += len(visited[char])

        return result
```

Method 2 (Hash Map + Set, Time Complexity: $O(N)$ (Because the maximum length of `set(s)` is 26, so `O(26*N)` -> `O(N)`), Space Complexity: $O(N)$) :
```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        mapping = defaultdict(list)
        for index, char in enumerate(s):
            mapping[char].append(index)

        result = 0
        for char in set(s):
            # Option 1
            index_left = mapping[char][0]
            index_right = mapping[char][-1]
            substring = set()
            for index_center in range(index_left+1, index_right):
                substring.add(s[index_center])

            result += len(substring)
            """
            # Option 2

            result += len(set(s[mapping[char][0]+1:mapping[char][-1]]))
            """

        return result
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        result = 0
        for char in set(s):
            index_left = s.find(char)
            index_right = s.rfind(char)
            substring = set()
            for index in range(index_left+1, index_right):
                substring.add(s[index])

            result += len(substring)

        return result
```
