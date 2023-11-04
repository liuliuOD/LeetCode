![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1503. [Last Moment Before All Ants Fall Out Of A Plank](https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn get_last_moment(n: i32, left: Vec<i32>, right: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        for item in left {
            result = result.max(item);
        }

        for item in right {
            result = result.max(n - item);
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn get_last_moment(n: i32, left: Vec<i32>, right: Vec<i32>) -> i32 {
        /* Option 1 */
        let mut result: i32 = match left.iter().max() {
            Some(&max) => max,
            None => 0,
        };
        /* Option 2

        let mut result: i32 = *left.iter().max().unwrap_or(&0);
        */

        for item in right {
            result = result.max(n - item);
        }

        return result
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn get_last_moment(n: i32, left: Vec<i32>, right: Vec<i32>) -> i32 {
        return (*left.iter().max().unwrap_or(&0)).max(right.iter().map(|value| n - value).max().unwrap_or(0))
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N+M)$ (N: length of `left`, M: length of `right`), Space Complexity: $O(1)$) :
```python
class Solution:
    def getLastMoment(self, n: int, left: List[int], right: List[int]) -> int:
        result = 0
        for item in left:
            result = max(result, item)

        for item in right:
            result = max(result, n - item)

        return result
```
