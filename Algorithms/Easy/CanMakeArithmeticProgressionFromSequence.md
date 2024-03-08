![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1502. [Can Make Arithmetic Progression From Sequence](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn can_make_arithmetic_progression(mut arr: Vec<i32>) -> bool {
        arr.sort();
        let mut origin = arr[1];
        let mut difference = origin - arr[0];
        for index in 2..arr.len() {
            if difference != arr[index] - origin {
                return false
            }
            origin = arr[index];
        }

        return true
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def canMakeArithmeticProgression(self, arr: List[int]) -> bool:
        previous = None
        difference = None
        for item in sorted(arr):
            if previous is not None and difference is not None and difference != (item - previous):
                return False
            difference = item - previous if previous is not None else None
            previous = item
        return True
```
