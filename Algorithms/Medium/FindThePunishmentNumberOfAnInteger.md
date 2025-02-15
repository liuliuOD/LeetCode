![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2698. [Find The Punishment Number Of An Integer](https://leetcode.com/problems/find-the-punishment-number-of-an-integer)

### Solution :

Method 1 (DFS, Time Complexity: $O(N*2^{log_{10}(N)})$, Space Complexity: $O(log_{10}(N))$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn punishment_number(n: i32) -> i32 {
        let mut result: i32 = 0;
        for num in 1..=n {
            if Self::can_partition(num*num, num) {
                result += num*num;
            }
        }

        return result
    }

    fn can_partition(origin: i32, target: i32) -> bool {
        if origin == target {
            return true
        }
        if origin < target || target < 0 {
            return false
        }

        return Self::can_partition(origin / 10, target - (origin%10))
            || Self::can_partition(origin / 100, target - (origin%100))
            || Self::can_partition(origin / 1000, target - (origin%1000))
    }
}
```

### Solution :

Method 1 (In weekly contest 346, DFS) :
```python
class Solution:
    def punishmentNumber(self, n: int) -> int:
        result = 0
        for i in range(1, n+1):
            result += self.findNumber(i)

        return result

    def findNumber(self, i: int) -> int:
        power = i*i
        if self.valid(i, str(power)):
            return power
        return 0

    def valid(self, target: int, power: str) -> bool:
        for i in range(1, len(power)+1):
            if self.dfs(int(power[:i]), target, power[i:]):
                return True
        return False

    def dfs(self, value: int, target: int, s: str) -> bool:
        if len(s) == 0:
            return value == target
        if value + int(s) == target:
            return True
        for i in range(1, len(s)+1):
            if self.dfs(value+int(s[:i]), target, s[i:]):
                return True

        return False
```
