![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2109. [Adding Spaces To A String](https://leetcode.com/problems/adding-spaces-to-a-string)

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the length of `s`, N: the length of `spaces`)) :
```rust
impl Solution {
    pub fn add_spaces(s: String, spaces: Vec<i32>) -> String {
        let n: usize = s.len();
        let s_char: Vec<char> = s.chars().collect::<Vec<char>>();
        let mut index: usize = 0;
        let mut result: String = String::new();
        for index_space in spaces {
            let index_space: usize = index_space as usize;
            while index < n && index < index_space {
                result.push(s_char[index]);
                index += 1;
            }

            result.push_str(&" ");
        }

        while index < n {
            result.push(s_char[index]);
            index += 1;
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the length of `s`, N: the length of `spaces`)) :
```rust
impl Solution {
    pub fn add_spaces(s: String, spaces: Vec<i32>) -> String {
        let mut result: String = String::new();
        let mut index_space: usize = 0;
        for (index, character) in s.chars().enumerate() {
            if index_space < spaces.len() && index == spaces[index_space] as usize {
                result.push_str(&" ");
                index_space += 1;
            }

            result.push(character);
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the length of `s`, N: the length of `spaces`)) :
```java
class Solution {
    public String addSpaces(String s, int[] spaces) {
        int m = s.length();
        int n = spaces.length;
        int index_spaces = 0;
        StringBuilder result = new StringBuilder();
        for (int index_s=0; index_s<m; index_s++) {
            if (index_spaces < n && index_s == spaces[index_spaces]) {
                result.append(" ");
                index_spaces++;
            }

            result.append(s.charAt(index_s));
        }

        return result.toString();
    }
}
```
