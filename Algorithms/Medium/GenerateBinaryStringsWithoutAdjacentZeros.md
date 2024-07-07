![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3211. [Generate Binary Strings Without Adjacent Zeros](https://leetcode.com/problems/generate-binary-strings-without-adjacent-zeros)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(2^N)$ (N: value of `n`)) :
```rust
impl Solution {
    pub fn valid_strings(n: i32) -> Vec<String> {
        if n == 1 {
            return vec!["0".to_string(), "1".to_string()]
        }

        let mut result: Vec<String> = vec![];
        let mut base: String = String::new();
        Self::backtracking(&mut base, &mut result, n as usize);

        return result
    }

    fn backtracking(base: &mut String, result: &mut Vec<String>, n: usize) {
        if base.len() >= n {
            result.push(base.to_string());
            return
        }

        *base += "1";
        Self::backtracking(base, result, n);
        base.pop();
        if base.len() == 0 || base[base.len()-1..] == *"1" {
            *base += "0";
            Self::backtracking(base, result, n);
            base.pop();
        }
    }
}
```
