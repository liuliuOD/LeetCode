![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1716. [Calculate Money In Leetcode Bank](https://leetcode.com/problems/calculate-money-in-leetcode-bank)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn total_money(mut n: i32) -> i32 {
        let mut base: i32 = 1;
        let mut result: i32 = 0;
        while n > 0 {
            for offset in 0..=6 {
                if n <= 0 {
                    break;
                }
                n -= 1;

                result += base + offset;
            }

            base += 1;
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn total_money(mut n: i32) -> i32 {
        let amount_full_week: i32 = n / 7;
        let week_first: i32 = (1..=7).sum();
        let mut result: i32 = (week_first*2+(amount_full_week-1)*7) * amount_full_week / 2;
        if n % 7 != 0 {
            result += (1..=(n%7)).sum::<i32>() + (n%7)*amount_full_week;
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def totalMoney(self, n: int) -> int:
        result = 0
        base = 0
        while n:
            base += 1
            for offset in range(7):
                if n <= 0:
                    break

                result += base + offset
                n -= 1

        return result
```

Method 2 :
```python
class Solution:
    def totalMoney(self, n: int) -> int:
        return sum(list(range(1, 8)))*(n//7) + sum(list(range(1, n%7+1))) + (sum(list(range(1, n//7)))*7+(n%7)*(n//7) if n > 7 else 0)
```
