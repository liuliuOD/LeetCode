![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3075. [Maximize Happiness Of Selected Children](https://leetcode.com/problems/maximize-happiness-of-selected-children)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn maximum_happiness_sum(mut happiness: Vec<i32>, k: i32) -> i64 {
        happiness.sort();
        let mut result: i64 = 0;
        for turn in 0..k {
            let maximum: i32 = happiness.pop().unwrap();
            if maximum > turn {
                result += (maximum - turn) as i64;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumHappinessSum(self, happiness: List[int], k: int) -> int:
        happiness.sort()
        turn = 0
        result = 0
        while turn < k:
            result += max(0, happiness.pop() - turn)
            turn += 1

        return result
```
