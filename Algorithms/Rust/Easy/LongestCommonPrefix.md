## [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix)

### Solution :

Method 1 (time complexity: O(n**2)):
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

        result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn longest_common_prefix(strs: Vec<String>) -> String {
        strs.into_iter().reduce(|acc, item| {
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
        strs.iter().skip(1).fold(strs[0].clone(), |acc, item| {
            acc.chars()
                .zip(item.chars())
                .take_while(|(a, b)| a == b)
                .map(|(a, _)| a)
                .collect()
        })
    }
}
```
