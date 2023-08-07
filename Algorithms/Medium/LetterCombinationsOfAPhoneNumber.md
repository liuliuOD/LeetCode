![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 17. [Letter Combinations Of A Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)

### Solution :

Method 1 (Iterative DFS) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn letter_combinations(digits: String) -> Vec<String> {
        let mapping: HashMap<char, &str> = [
            ('2', "abc"),
            ('3', "def"),
            ('4', "ghi"),
            ('5', "jkl"),
            ('6', "mno"),
            ('7', "pqrs"),
            ('8', "tuv"),
            ('9', "wxyz"),
        ].into();

        let mut result: Vec<String> = vec![];
        if digits.is_empty() {
            return result
        }

        let mut stack: Vec<(usize, String)> = vec![(0, String::new())];
        while !stack.is_empty() {
            let (index_digit, combination) = stack.pop().unwrap();

            if combination.len() == digits.len() {
                result.push(combination.to_string().clone());
                continue;
            }

            for letter in mapping[&(digits.as_bytes()[index_digit] as char)].chars() {
                stack.push((index_digit+1, combination.clone() + &letter.to_string()));
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Recursive DFS) :
```python
class Solution:
    def __init__(self):
        self.mapping = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z'],
        }

    def letterCombinations(self, digits: str) -> List[str]:
        result: List[str] = []
        if len(digits) > 0:
            self.dfs('', result, 0, digits)

        return result

    def dfs(self, combination: str, result: List[str], index_digit: int, digits: str):
        if index_digit == len(digits):
            result.append(combination)
            return None

        for letter in self.mapping[digits[index_digit]]:
            self.dfs(combination+letter, result, index_digit+1, digits)
```

Method 2 (Iterative DFS) :
```python
class Solution:
    def __init__(self):
        self.mapping = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z'],
        }

    def letterCombinations(self, digits: str) -> List[str]:
        result: List[str] = []
        if len(digits) == 0:
            return result

        stack = [(0, '')]
        while stack:
            index_digit, combination = stack.pop()

            if len(combination) == len(digits):
                result.append(combination)
                continue

            for letter in self.mapping[digits[index_digit]]:
                stack.append((index_digit+1, combination+letter))

        return result
```

Method 3 (BFS) :
```python
class Solution:
    def __init__(self):
        self.mapping = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z'],
        }

    def letterCombinations(self, digits: str) -> List[str]:
        result: List[str] = []
        if len(digits) == 0:
            return result

        queue = deque([(0, '')])
        while queue:
            index_digit, combination = queue.popleft()

            if len(combination) == len(digits):
                result.append(combination)
                continue

            for letter in self.mapping[digits[index_digit]]:
                queue.append((index_digit+1, combination+letter))

        return result
```
