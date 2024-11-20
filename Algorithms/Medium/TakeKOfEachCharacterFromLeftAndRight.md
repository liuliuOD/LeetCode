![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2516. [Take K Of Each Character From Left And Right](https://leetcode.com/problems/take-k-of-each-character-from-left-and-right)

### Solution :

Method 1 (Binary Search + Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
use std::collections::HashSet;
const BASE: u8 = b'a';
impl Solution {
    pub fn take_characters(s: String, k: i32) -> i32 {
        let s_bytes: Vec<u8> = s.as_bytes().to_vec();
        let mut visited: [i32; 3] = [0; 3];
        for ascii in s_bytes.iter() {
            visited[(ascii-BASE) as usize] += 1;
        }
        for index in 0..3 {
            if visited[index] < k {
                return -1
            }
        }

        let n: usize = s.len();
        let mut left: usize = 1;
        let mut right: usize = n;
        while left <= right && right <= n {
            let window: usize = left + (right-left)/2;
            let mut visited_temp: [i32; 3] = visited.clone();
            let mut valid: bool = false;
            for index in 0..n {
                visited_temp[(s_bytes[index]-BASE) as usize] -= 1;
                if index >= window {
                    visited_temp[(s_bytes[index-window]-BASE) as usize] += 1;
                }

                if index >= window-1 && visited_temp[0] >= k && visited_temp[1] >= k && visited_temp[2] >= k {
                    valid = true;
                    break;
                }
            }

            if valid {
                left = window + 1;
            } else {
                right = window - 1;
            }
        }

        return match right <= n {
            true => (n - right) as i32,
            false => n as i32,
        }
    }
}
```
