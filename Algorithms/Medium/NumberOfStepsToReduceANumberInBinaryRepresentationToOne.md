![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1404. [Number Of Steps To Reduce A Number In Binary Representation To One](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one)

### Solution :

Method 1 (Bitwise + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
const ZERO: i32 = '0' as i32;

impl Solution {
    pub fn num_steps(s: String) -> i32 {
        let s: Vec<u8> = s.into_bytes();
        let mut carry: i32 = 0;
        let mut result: i32 = 0;
        for index in (1..s.len()).rev() {
            let bit: i32 = s[index] as i32 - ZERO + carry;
            match bit % 2 {
                1 => {
                    result += 2;
                    carry = 1;
                },
                _ => result += 1,
            };
        }

        return result + carry
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numSteps(self, s: str) -> int:
        decimal = int(s, 2)
        result = 0
        while decimal > 1:
            if decimal % 2 == 0:
                decimal //= 2
            else:
                decimal += 1

            result += 1

        return result
```

Method 2 (Bitwise, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numSteps(self, s: str) -> int:
        carry: bool = False
        result = 0
        for index in reversed(range(len(s))):
            if index == 0:
                if carry:
                    result += 1
                break

            if s[index] == "1":
                if carry:
                    result += 1
                else:
                    result += 2

                carry = True
            elif s[index] == "0":
                if carry:
                    result += 2
                else:
                    result += 1
                    carry = False

        return result
```

Method 3 (Bitwise + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numSteps(self, s: str) -> int:
        carry = 0
        result = 0
        for index in reversed(range(1, len(s))):
            bit = int(s[index]) + carry
            if bit % 2 == 1:
                result += 2
                carry = 1
            else:
                result += 1

        return result + carry
```

### Solution :

Method 1 (Bitwise + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
const BASE int = int('0')

func numSteps(s string) int {
    var carry int
    var result int
    for index := len(s)-1; index >= 1; index-- {
        bit := int(s[index]) - BASE + carry
        if bit % 2 == 1 {
            result += 2
            carry = 1
        } else {
            result += 1
        }
    }

    return result + carry
}
```
