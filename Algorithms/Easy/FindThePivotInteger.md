![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2485. [Find The Pivot Integer](https://leetcode.com/problems/find-the-pivot-integer)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn pivot_integer(n: i32) -> i32 {
        let mut total: i32 = (1..=n).sum();
        let mut current: i32 = 0;
        for num in 1..=n {
            current += num;
            if current == total {
                return num
            }

            total -= num;
        }

        return -1
    }
}
```

Method 2 (Mathematic, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn pivot_integer(n: i32) -> i32 {
        let total: i32 = n*(n + 1) / 2;

        let square_root: i32 = (total as f64).sqrt() as i32;

        return match square_root.pow(2) == total {
            true => square_root,
            false => -1,
        }
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def pivotInteger(self, n: int) -> int:
        pivot = 1
        left = pivot
        right = sum(range(1, n+1))
        while left != right and pivot <= n:
            pivot += 1
            left += pivot
            right -= (pivot - 1)

        return pivot if pivot <= n else -1
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func pivotInteger(n int) int {
    left := 0
    right := 0
    for i := 1; i <= n; i++ {
        right += i
    }

    for pivot := 1; pivot <= n; pivot++ {
        right -= pivot
        if left == right {
            return pivot
        }
        left += pivot
    }

    return -1
}
```

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func pivotInteger(n int) int {
    left := 0
    right := n + 1
    leftSum := 0
    rightSum := 0
    for left < right {
        if leftSum < rightSum {
            left++
            leftSum += left
        } else if leftSum > rightSum {
            right--
            rightSum += right
        } else if left+1 == right-1 {
            return left + 1
        } else {
            left++
            leftSum += left
        }
    }

    return -1
}
```
