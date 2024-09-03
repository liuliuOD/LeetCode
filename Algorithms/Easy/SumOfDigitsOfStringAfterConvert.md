![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1945. [Sum Of Digits Of String After Convert](https://leetcode.com/problems/sum-of-digits-of-string-after-convert)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the nodes in the tree)) :
```Rust
impl Solution {
    pub fn get_lucky(s: String, mut k: i32) -> i32 {
        let mut result: i32 = 0;
        for byte in s.bytes() {
            let mut alphabet: i32 = (byte - b'a' + 1) as i32;

            while alphabet > 0 {
                result += alphabet % 10;
                alphabet /= 10;
            }
        }

        k -= 1;
        while k > 0 {
            k -= 1;
            let mut temp: i32 = result;
            result = 0;
            while temp > 0 {
                result += temp % 10;
                temp /= 10;
            }
        }

        return result
    }
}
```
