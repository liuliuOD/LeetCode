![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1137. [Nth Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
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

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn tribonacci(n: i32) -> i32 {
        let mut candidates: [i32; 3] = [0, 1, 1];
        if n <= 2 {
            return candidates[n as usize]
        }

        for _ in 3..=n {
            let temp: i32 = candidates[0] + candidates[1] + candidates[2];
            candidates[0] = candidates[1];
            candidates[1] = candidates[2];
            candidates[2] = temp;
        }

        return candidates[2]
    }
}
```

Method 3 (Queue, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
use std::collections::VecDeque;
impl Solution {
    pub fn tribonacci(n: i32) -> i32 {
        let mut queue: VecDeque<i32> = VecDeque::from([0, 1, 1]);
        if n <= 2 {
            return queue[n as usize]
        }

        for _ in 3..=n {
            queue.push_back(queue[0] + queue[1] + queue[2]);
            queue.pop_front();
        }

        return *queue.back().unwrap()
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

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def tribonacci(self, n: int) -> int:
        memoization = [0, 1, 1]
        for i in range(3, n+1):
            memoization.append(memoization[i-1] + memoization[i-2] + memoization[i-3])
        return memoization[n]
```

Method 3 (Queue, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def tribonacci(self, n: int) -> int:
        queue = deque([0, 1, 1])
        if n <= 2:
            return queue[n]

        for _ in range(3, n+1):
            queue.append(queue[0] + queue[1] + queue[2])
            queue.popleft()

        return queue[2]
```

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func tribonacci(n int) int {
    var a, b, c int = 0, 1, 1
    if n <= 2 {
        return []int{a, b, c}[n]
    }

    for index := 3; index <= n; index++ {
        temp := a + b + c
        a, b, c = b, c, temp
    }
    return c
}
```
