![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 14. [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix)

### Solution :

Method 1 (Time Complexity: $O(N^2)$):
```rust
impl Solution {
    pub fn longest_common_prefix(strs: Vec<String>) -> String {
        let mut result = "".to_string();
        for index in 0..200 {
            let mut valid = true;
            for item in &strs {
                if item.len() <= index || strs[0].len() <= index || item[index..index+1] != strs[0][index..index+1] {
                    valid = false;
                    break;
                }
            }

            if !valid {
                break;
            }
            result.push_str(&strs[0][index..index+1]);
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn longest_common_prefix(strs: Vec<String>) -> String {
        return strs.into_iter().reduce(|acc, item| {
            acc.chars()
                .zip(item.chars())
                .take_while(|(a, b)| a == b)
                .map(|(a, _)| a)
                .collect()
        }).unwrap()
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn longest_common_prefix(strs: Vec<String>) -> String {
        return strs.iter().skip(1).fold(strs[0].clone(), |acc, item| {
            acc.chars()
                .zip(item.chars())
                .take_while(|(a, b)| a == b)
                .map(|(a, _)| a)
                .collect()
        })
    }
}
```

### Solution :

Method 1 (Trie Tree) :
```python
class Node:
    def __init__(self):
        self.amount = 1
        self.children = {}

class Trie:
    def __init__(self, n):
        self.root = Node()
        self.result = 0
        self.n = n

    def add(self, string: str):
        result = 0
        node = self.root
        for char in string:
            if char not in node.children:
                node.children[char] = Node()
            else:
                node.children[char].amount += 1

            result += node.children[char].amount == self.n
            node = node.children[char]

        self.result = result

class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        trie = Trie(len(strs))
        for string in strs:
            trie.add(string)

        return strs[0][:trie.result]
```

Method 2 :
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        result = ''
        index = 0
        while True:
            is_valid = True
            for string in strs:
                if index >= len(string) or string[index] != strs[0][index]:
                    is_valid = False
                    break

            if is_valid:
                result += strs[0][index]
                index += 1
                continue

            break

        return result
```
