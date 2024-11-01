![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1957. [Delete Characters To Make Fancy String](https://leetcode.com/problems/delete-characters-to-make-fancy-string)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `s`)) :
```Rust
impl Solution {
    pub fn make_fancy_string(s: String) -> String {
        let n: usize = s.len();
        let s_chars: Vec<char> = s.chars().collect::<Vec<char>>();
        let mut result: String = s_chars[0].to_string();
        let mut char_previous: char = s_chars[0];
        let mut cumulative_times: usize = 1;
        for index in 1..n {
            match s_chars[index] == char_previous {
                true => {
                    cumulative_times += 1;
                    if cumulative_times >= 3 {
                        continue;
                    }
                },
                false => {
                    char_previous = s_chars[index];
                    cumulative_times = 1;
                },
            };

            result += &s_chars[index].to_string();
        }

        return result
    }
}
```

Method 2 (Built-In methods, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `s`)) :
```rust
impl Solution {
    pub fn make_fancy_string(s: String) -> String {
        return s.as_bytes()
            .chunk_by(|a, b| a == b)
            .flat_map(|chunk| chunk.iter().take(2).map(|item| *item as char))
            .collect()
    }
}
```

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 303/306, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `s`)) :
```java
class Solution {
    public String makeFancyString(String s) {
        int n = s.length();
        String char_previous = s.substring(0, 1);
        String result = new String(char_previous);
        int cumulative_times = 1;
        for (int index=1; index<n; index++) {
            if (s.substring(index, index+1).equals(char_previous)) {
                cumulative_times += 1;
                if (cumulative_times >= 3) {
                    continue;
                }
            } else {
                char_previous = s.substring(index, index+1);
                cumulative_times = 1;
            }

            result = result.concat(char_previous);
        }

        return result;
    }
}
```

Method 2 (String Builder, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `s`)) :
```java
class Solution {
    public String makeFancyString(String s) {
        int n = s.length();
        String char_previous = s.substring(0, 1);
        StringBuilder result = new StringBuilder(char_previous);
        int cumulative_times = 1;
        for (int index=1; index<n; index++) {
            if (s.substring(index, index+1).equals(char_previous)) {
                cumulative_times += 1;
                if (cumulative_times >= 3) {
                    continue;
                }
            } else {
                char_previous = s.substring(index, index+1);
                cumulative_times = 1;
            }

            result.append(char_previous);
        }

        return result.toString();
    }
}
```
