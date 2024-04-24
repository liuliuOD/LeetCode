![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1201. [Ugly Number III](https://leetcode.com/problems/ugly-number-iii)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(Log(N))$ (N: 2*10^9), Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn nth_ugly_number(n: i32, a: i32, b: i32, c: i32) -> i32 {
        let n: i64 = n as i64;
        let a: i64 = a as i64;
        let b: i64 = b as i64;
        let c: i64 = c as i64;
        let mut left: i64 = 1;
        let mut right: i64 = 2_000_000_000;
        while left <= right {
            let middle: i64 = left + (right - left) / 2;
            let amount: i64 = Self::amount(middle, a, b, c);
            if amount < n {
                left = middle + 1;
            } else {
                right = middle - 1;
            }
        }

        return left as i32
    }

    fn gcd(m: i64, n: i64) -> i64 {
        if m == 0 {
            return n
        }
        return Self::gcd(n%m, m)
    }

    fn lcm(m: i64, n: i64) -> i64 {
        return ((m as i64 * n as i64) / Self::gcd(m, n)) as i64
    }

    fn amount(num: i64, a: i64, b: i64, c: i64) -> i64 {
        return num / a + num / b + num / c - (num / Self::lcm(a, b) + num / Self::lcm(a, c) + num / Self::lcm(b, c)) + num / Self::lcm(Self::lcm(a, b), c)
    }
}
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(Log(N))$ (N: 2*10^9), Space Complexity: $O(1)$) :
```python
class Solution:
    def nthUglyNumber(self, n: int, a: int, b: int, c: int) -> int:
        left, right = 1, 2_000_000_000
        while left <= right:
            middle = left + (right - left) // 2

            amount = middle // a + middle // b + middle // c - middle // self.get_lcm(a, b) - middle // self.get_lcm(b, c) - middle // self.get_lcm(a, c) + middle // self.get_lcm(self.get_lcm(a, b), c)
            if amount < n:
                left = middle + 1
            else:
                right = middle - 1

        return left

    def get_gcd(self, a: int, b: int) -> int:
        if a == 0:
            return b
        return self.get_gcd(b%a, a)

    def get_lcm(self, a: int, b: int) -> int:
        return a * b // self.get_gcd(a, b)
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(Log(N))$ (N: 2*10^9), Space Complexity: $O(1)$) :
```go
func nthUglyNumber(n int, a int, b int, c int) int {
    left, right := 1, 2_000_000_000
    for left <= right {
        middle := left + (right - left) / 2
        amount := getAmount(middle, a, b, c)
        if amount < n {
            left = middle + 1
        } else {
            right = middle - 1
        }
    }

    return left
}

func getAmount(num, a, b, c int) int {
    return num / a + num / b + num / c - (num / lcm(a, b) + num / lcm(a, c) + num / lcm(b, c)) + num / lcm(lcm(a, b), c)
}

func lcm(m, n int) int {
    return m*n / gcd(m, n)
}

func gcd(m, n int) int {
    if m == 0 {
        return n
    }
    return gcd(n%m, m)
}
```

Method 2 (Binary Search, Time Complexity: $O(Log(N))$ (N: 2*10^9), Space Complexity: $O(1)$) :
```go
func nthUglyNumber(n int, a int, b int, c int) int {
    ab, bc, ac, abc := lcm(a, b), lcm(b, c), lcm(a, c), lcm(lcm(a, b), c)

    left, right := 1, 2_000_000_000
    for left <= right {
        middle := left + (right - left) / 2
        amount := getAmount(middle, a, b, c, ab, bc, ac, abc)
        if amount < n {
            left = middle + 1
        } else {
            right = middle - 1
        }
    }

    return left
}

func getAmount(num, a, b, c, ab, bc, ac, abc int) int {
    return num / a + num / b + num / c - (num / ab + num / ac + num / bc) + num / abc
}

func lcm(m, n int) int {
    return m*n / gcd(m, n)
}

func gcd(m, n int) int {
    if m == 0 {
        return n
    }
    return gcd(n%m, m)
}
```
