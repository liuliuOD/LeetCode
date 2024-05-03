![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 165. [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers)

### Solution :

Method 1 (Time Complexity: $O(N)$ (N: length of the longest param), Space Complexity: $O(1)$) :
```rust
use std::cmp::Ordering;
const POINT: u8 = '.' as u8;
const ZERO: u8 = '0' as u8;
impl Solution {
    pub fn compare_version(mut version1: String, mut version2: String) -> i32 {
        let mut bytes1 = version1.bytes();
        let mut bytes2 = version2.bytes();
        let mut number1: i32 = 0;
        let mut number2: i32 = 0;
        let mut is_none1: bool = false;
        let mut is_none2: bool = false;
        loop {
            while let current1 = bytes1.next() {
                match current1 {
                    None => {
                        is_none1 = true;
                        break;
                    },
                    Some(byte) => {
                        if byte == POINT {
                            break;
                        }
                        number1 = number1 * 10 + (byte - ZERO) as i32;
                    }
                }
            }

            while let current2 = bytes2.next() {
                match current2 {
                    None => {
                        is_none2 = true;
                        break;
                    },
                    Some(byte) => {
                        if byte == POINT {
                            break;
                        }
                        number2 = number2 * 10 + (byte - ZERO) as i32;
                    }
                }
            }

            if number1 != number2 {
                break;
            }
            number1 = 0;
            number2 = 0;
            if is_none1 && is_none2 {
                break;
            }
        }

        return match number1.cmp(&number2) {
            Ordering::Equal => 0,
            Ordering::Greater => 1,
            Ordering::Less => -1,
        }
    }
}
```

### Solution :

Method 1 (Hash Map + Bitwise, Time Complexity: $O(N)$ (N: length of the longest param), Space Complexity: $O(N)$) :
```python
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        version1 = version1.split(".")
        version2 = version2.split(".")
        n1, n2 = len(version1), len(version2)
        index1 = index2 = 0
        while index1 < n1 or index2 < n2:
            num1 = num2 = 0
            if index1 < n1:
                num1 = int(version1[index1])
            if index2 < n2:
                num2 = int(version2[index2])

            if num1 > num2:
                return 1
            elif num1 < num2:
                return -1

            index1 += 1
            index2 += 1

        return 0
```
