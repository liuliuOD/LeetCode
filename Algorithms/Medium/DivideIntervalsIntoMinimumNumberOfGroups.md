![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2406. [Divide Intervals Into Minimum Number Of Groups](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups)

### Solution :

Method 1 (Sorted, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `intervals`)) :
```rust
impl Solution {
    pub fn min_groups(intervals: Vec<Vec<i32>>) -> i32 {
        let n: usize = intervals.len();
        let mut times: Vec<(i32, i32)> = Vec::with_capacity(n);
        for interval in intervals {
            times.push((interval[0], 1));
            times.push((interval[1]+1, -1));
        }

        times.sort();
        let mut result: i32 = 0;
        let mut amount_concurrent_interval: i32 = 0;
        for time in times {
            amount_concurrent_interval += time.1;
            result = i32::max(result, amount_concurrent_interval);
        }

        return result
    }
}
```
