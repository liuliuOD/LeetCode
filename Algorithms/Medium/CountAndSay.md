![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 38. [Count And Say](https://leetcode.com/problems/count-and-say)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(M*N)$, Space Complexity: $O(M)$ (M: the length of the string at each step, N: the value of `n`)) :
```rust
impl Solution {
    pub fn count_and_say(n: i32) -> String {
        let mut res = String::from("1");

        for _ in 0..(n - 1) {
            let mut temp = String::new();
            let mut i = 0;
            let chars: Vec<char> = res.chars().collect();

            while i < chars.len() {
                let mut count = 1;
                while i + 1 < chars.len() && chars[i] == chars[i + 1] {
                    i += 1;
                    count += 1;
                }
                temp.push_str(&count.to_string());
                temp.push(chars[i]);
                i += 1;
            }

            res = temp;
        }

        return res
    }
}
```
