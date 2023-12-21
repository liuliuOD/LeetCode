![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1637. [Widest Vertical Area Between Two Points Containing No Points](https://leetcode.com/problems/widest-vertical-area-between-two-points-containing-no-points)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_width_of_vertical_area(mut points: Vec<Vec<i32>>) -> i32 {
        points.sort();
        let n: usize = points.len();
        let mut result: i32 = 0;
        /* Option 1 */
        for index in 1..n {
            result = result.max(points[index][0]-points[index-1][0]);
        }
        /* Option 2

        (1..n).for_each(|index| result = result.max(points[index][0]-points[index-1][0]));
        */

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxWidthOfVerticalArea(self, points: List[List[int]]) -> int:
        points.sort()
        n = len(points)
        result = 0
        for index in range(1, n):
            result = max(result, points[index][0] - points[index-1][0])

        return result
```
