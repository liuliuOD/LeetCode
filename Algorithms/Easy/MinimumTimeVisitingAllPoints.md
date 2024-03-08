![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1266. [Minimum Time Visiting All Points](https://leetcode.com/problems/minimum-time-visiting-all-points)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_time_to_visit_all_points(points: Vec<Vec<i32>>) -> i32 {
        return points.windows(2).map(|window| (window[0][0]-window[1][0]).abs().max((window[0][1]-window[1][1]).abs())).sum()
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def minTimeToVisitAllPoints(self, points: List[List[int]]) -> int:
        return sum([max(abs(points[index-1][0] - points[index][0]), abs(points[index-1][1] - points[index][1])) for index in range(1, len(points))])
```
