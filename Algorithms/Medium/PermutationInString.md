![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 567. [Permutation In String](https://leetcode.com/problems/permutation-in-string)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (N: the length of `s1`, M: the length of `s2`)) :
```rust
const BASE: usize = 'a' as usize;
impl Solution {
    pub fn check_inclusion(s1: String, s2: String) -> bool {
        let mut counter: [i32; 26] = [0; 26];
        for character in s1.chars() {
            counter[character as usize - BASE] += 1;
        }

        let n: usize = s1.len();
        let mut counter_s2: [i32; 26] = [0; 26];
        let s2_bytes: Vec<u8> = s2.into_bytes();
        for (index, &character) in s2_bytes.iter().enumerate() {
            counter_s2[character as usize - BASE] += 1;

            if index >= n {
                counter_s2[s2_bytes[index-n] as usize - BASE] -= 1;
            }

            let mut is_contain: bool = true;
            for (index, &amount) in counter.iter().enumerate() {
                if amount != counter_s2[index] {
                    is_contain = false;
                    break;
                }
            }

            if is_contain {
                return true
            }
        }

        return false
    }
}
```

Method 2 (Sliding Window + Optimization, Time Complexity: $O(M)$, Space Complexity: $O(1)$ (M: the length of `s2`)) :
```rust
const BASE: usize = 'a' as usize;
impl Solution {
    pub fn check_inclusion(s1: String, s2: String) -> bool {
        let m: usize = s2.len();
        let n: usize = s1.len();
        if m < n {
            return false
        }

        let s1_bytes: Vec<u8> = s1.into_bytes();
        let s2_bytes: Vec<u8> = s2.into_bytes();
        let mut counter_s1: [i32; 26] = [0; 26];
        let mut counter_s2: [i32; 26] = [0; 26];
        for index in 0..n {
            counter_s1[s1_bytes[index] as usize - BASE] += 1;
            counter_s2[s2_bytes[index] as usize - BASE] += 1;
        }

        let mut amount_the_same: i8 = 0;
        for index in 0..26 {
            if counter_s1[index] == counter_s2[index] {
                amount_the_same += 1;
            }
        }

        if amount_the_same == 26 {
            return true
        }

        for index_right in n..m {
            let offset_right: usize = s2_bytes[index_right] as usize - BASE;
            counter_s2[offset_right] += 1;
            if counter_s2[offset_right] == counter_s1[offset_right] {
                amount_the_same += 1;
            } else if counter_s2[offset_right]-1 == counter_s1[offset_right] {
                amount_the_same -= 1;
            }

            let index_left: usize = index_right - n;
            let offset_left: usize = s2_bytes[index_left] as usize - BASE;
            counter_s2[offset_left] -= 1;
            if counter_s2[offset_left] == counter_s1[offset_left] {
                amount_the_same += 1;
            } else if counter_s2[offset_left]+1 == counter_s1[offset_left] {
                amount_the_same -= 1;
            }

            if amount_the_same == 26 {
                return true
            }
        }

        return false
    }
}
```
