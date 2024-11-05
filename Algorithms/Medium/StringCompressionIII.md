![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 3163. [String Compression III](https://leetcode.com/problems/string-compression-iii)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        let mut word_char: Vec<char> = word.chars().collect();
        word_char.push('?');
        let n: usize = word_char.len();
        let mut char_previous: char = word_char[0];
        let mut times: usize = 1;
        let mut result: String = String::new();
        for index in 1..n {
            let char_current: char = word_char[index];
            if times == 9 || char_previous != char_current {
                result += &(times.to_string() + &char_previous.to_string());
                times = 0;
                char_previous = char_current;
            }

            times += 1;
        }

        return result
    }
}
```

Method 2 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        let mut word_char: Vec<char> = word.chars().collect();
        word_char.push('?');
        let n: usize = word_char.len();
        let mut char_previous: char = word_char[0];
        let mut times: u32 = 1;
        let mut result: String = String::new();
        for index in 1..n {
            let char_current: char = word_char[index];
            if times == 9 || char_previous != char_current {
                result.push(char::from_digit(times, 10).unwrap());
                result.push(char_previous);

                times = 0;
                char_previous = char_current;
            }

            times += 1;
        }

        return result
    }
}
```

Method 3 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        return word.as_bytes()
            .chunk_by(|a, b| a == b)
            .flat_map(|group| {
                let mut result: Vec<char> = Vec::new();
                let mut n: u32 = group.len() as u32;
                while n > 0 {
                    result.push(char::from_digit(u32::min(n, 9), 10).unwrap());
                    result.push(group[0] as char);

                    n -= u32::min(n, 9);
                }

                return result
            })
            .collect()
    }
}
```

Method 4 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        return String::from_utf8(
            word.as_bytes()
            .chunk_by(|a, b| a == b)
            .flat_map(|group| {
                let mut result: Vec<u8> = Vec::new();
                let mut n: u32 = group.len() as u32;
                while n > 0 {
                    result.push(char::from_digit(u32::min(n, 9), 10).unwrap() as u8);
                    result.push(group[0]);

                    n -= u32::min(n, 9);
                }

                return result
            })
            .collect()
        )
        .unwrap()
    }
}
```

Method 5 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```rust
impl Solution {
    pub fn compressed_string(word: String) -> String {
        return String::from_utf8(
            word.as_bytes()
            .chunk_by(|a, b| a == b)
            .flat_map(|group| {
                let mut result: Vec<u8> = Vec::new();
                let mut n: u32 = group.len() as u32;
                while n > 0 {
                    // 0 -> '0'
                    result.push(u32::min(n, 9) as u8 + 48);
                    result.push(group[0]);

                    n -= u32::min(n, 9);
                }

                return result
            })
            .collect()
        )
        .unwrap()
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```java
class Solution {
    public String compressedString(String word) {
        word += "?";
        StringBuilder result = new StringBuilder();
        char char_previous = word.charAt(0);
        int times = 1;
        for (int index=1; index<word.length(); index++) {
            char char_current = word.charAt(index);
            if (times == 9 || char_previous != char_current) {
                /* option 1 */
                result.append((char) (times+'0'));
                /* Option 2

                result.append(times);
                */
                result.append(char_previous);

                times = 0;
                char_previous = char_current;
            }

            times += 1;
        }

        return result.toString();
    }
}
```

Method 2 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `word`)) :
```java
class Solution {
    public String compressedString(String word) {
        word += "?";
        StringBuilder result = new StringBuilder();
        char char_previous = word.charAt(0);
        int times = 1;
        for (int index=1; index<word.length(); index++) {
            char char_current = word.charAt(index);
            if (times == 9 || char_previous != char_current) {
                char[] temp = {(char) (times+'0'), char_previous};
                /* Option 1 */
                result.append(new String(temp));
                /* Option 2

                result.append(String.valueOf(temp));
                */

                times = 0;
                char_previous = char_current;
            }

            times += 1;
        }

        return result.toString();
    }
}
```
