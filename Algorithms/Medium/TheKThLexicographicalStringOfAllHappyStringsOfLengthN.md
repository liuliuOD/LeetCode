![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1415. [The k-th Lexicographical String Of All Happy Strings Of Length N](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(N*2^N)$, Space Complexity: $O(2^N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn get_happy_string(n: i32, k: i32) -> String {
        let mut candidates: Vec<String> = Vec::new();
        let mut happy: Vec<u8> = Vec::new();
        Self::backtracking(&mut happy, &mut candidates, n);

        return match candidates.len() < k as usize {
            true => "".to_string(),
            false => {
                candidates.sort();
                return candidates[k as usize - 1].clone()
            },
        }
    }

    fn backtracking(happy: &mut Vec<u8>, candidates: &mut Vec<String>, n: i32) {
        if n == 0 {
            candidates.push(String::from_utf8(happy.to_vec()).unwrap());
            return
        }

        for char_next in ['a', 'b', 'c'] {
            if happy.len() > 0 && happy[happy.len()-1] == char_next as u8 {
                continue;
            }

            happy.push(char_next as u8);
            Self::backtracking(happy, candidates, n-1);
            happy.pop();
        }
    }
}
```
