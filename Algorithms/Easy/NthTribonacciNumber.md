![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1137. [Nth Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number)

### Solution :

Method 1 (Dynamic Programming) :
```rust
impl Solution {
    pub fn tribonacci(n: i32) -> i32 {
        let n: usize = n as usize;
        let mut memoization: Vec<i32> = vec![0, 1, 1];
        for i in 3..n+1 {
            memoization.push(memoization[i-1] + memoization[i-2] + memoization[i-3]);
        }

        return memoization[n]
    }
}
```

### Solution :

Method 1 (Recursive, ERROR: "Time Limit Exceeded", 31/39) :
```python
class Solution:
    def tribonacci(self, n: int) -> int:
        if n == 0:
            return 0
        
        if n <= 2:
            return 1
        
        return self.tribonacci(n-1) + self.tribonacci(n-2) + self.tribonacci(n-3)
```

Method 1 (Dynamic Programming) :
```python
class Solution:
    def tribonacci(self, n: int) -> int:
        memoization = [0, 1, 1]
        for i in range(3, n+1):
            memoization.append(memoization[i-1] + memoization[i-2] + memoization[i-3])
        return memoization[n]
```
