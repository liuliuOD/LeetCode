![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2849. [Determine If A Cell Is Reachable At A Given Time](https://leetcode.com/problems/determine-if-a-cell-is-reachable-at-a-given-time)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn is_reachable_at_time(sx: i32, sy: i32, fx: i32, fy: i32, t: i32) -> bool {
        /* Option 1 */
        return if sx == fx && sy == fy {
            t != 1
        } else {
            (fx - sx).abs().max((fy - sy).abs()) <= t
        }
        /* Option 2

        if sx == fx && sy == fy {
            return t != 1
        }

        return (fx - sx).abs().max((fy - sy).abs()) <= t
        */
        /* Option 3

        let x: i32 = (fx - sx).abs();
        let y: i32 = (fy - sy).abs();
        return if x == 0 && y == 0 {
            t != 1
        } else {
            x.max(y) <= t
        }
        */
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isReachableAtTime(self, sx: int, sy: int, fx: int, fy: int, t: int) -> bool:
        if sx == fx and sy == fy:
            return t != 1

        maximum = max(abs(fx - sx), abs(fy - sy))
        return t >= maximum
```
