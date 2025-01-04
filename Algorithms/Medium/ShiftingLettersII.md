![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2381. [Shifting Letters II](https://leetcode.com/problems/shifting-letters-ii)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 37/39, Time Complexity: $O(M*P+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `shifts`, N: the length of `s`, P: the average length of each element in `shifts`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn shifting_letters(s: String, shifts: Vec<Vec<i32>>) -> String {
        let n: usize = s.len();
        let mut sum_shifts: Vec<i32> = vec![0; n];
        for shift in &shifts {
            for index in shift[0] as usize..=shift[1] as usize {
                if shift[2] == 0 {
                    sum_shifts[index] -= 1;
                    continue;
                }
                sum_shifts[index] += 1;
            }
        }

        let mut result: Vec<u8> = s.as_bytes().to_vec();
        for (index, offset) in sum_shifts.iter().enumerate() {
            result[index] = BASE + ((((result[index] - BASE) as i32 + offset) % 26 + 26) % 26) as u8;
        }
        return String::from_utf8_lossy(&result).to_string()
    }
}
```

Method 2 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `shifts`, N: the length of `s`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn shifting_letters(s: String, shifts: Vec<Vec<i32>>) -> String {
        let n: usize = s.len();
        let mut target_shifts: Vec<i32> = vec![0; n];
        for shift in &shifts {
            let start: usize = shift[0] as usize;
            let end: usize = shift[1] as usize;
            let direction = shift[2];
            if direction == 0 {
                target_shifts[start] -= 1;
                if end < n-1 {
                    target_shifts[end+1] += 1;
                }
                continue;
            }

            target_shifts[start] += 1;
            if end < n-1 {
                target_shifts[end+1] -= 1;
            }
        }

        let mut result: Vec<u8> = s.as_bytes().to_vec();
        let mut offset_current: i32 = 0;
        for (index, offset) in target_shifts.iter().enumerate() {
            offset_current = (offset_current+offset) % 26;
            result[index] = BASE + ((((result[index]-BASE) as i32+offset_current)%26 + 26) % 26) as u8;
        }
        return String::from_utf8_lossy(&result).to_string()
    }
}
```
