![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
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

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `shifts`, N: the length of `s`)) :
```java
class Solution {
    private static final char BASE = 'a';
    public String shiftingLetters(String s, int[][] shifts) {
        int n = s.length();
        int[] prefixSum = new int[n];
        Arrays.fill(prefixSum, 0);
        for (int[] shift: shifts) {
            int start = shift[0];
            int end = shift[1];
            int direction = shift[2];
            switch (direction) {
                case 0:
                    prefixSum[start] -= 1;
                    if (end < n-1) {
                        prefixSum[end+1] += 1;
                    }
                    break;
                case 1:
                    prefixSum[start] += 1;
                    if (end < n-1) {
                        prefixSum[end+1] -= 1;
                    }
                    break;
                default:
            }
        }

        StringBuilder builder = new StringBuilder();
        int offset = 0;
        for (int index=0; index<n; index++) {
            char current = s.charAt(index);
            offset += prefixSum[index];
            builder.append((char) (((current-BASE+offset)%26 + 26)%26 + BASE));
        }

        return builder.toString();
    }
}
```
