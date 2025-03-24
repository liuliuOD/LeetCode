![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3169. [Count Days Without Meetings](https://leetcode.com/problems/count-days-without-meetings)

### Solution :

Method 1 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of elements in `meetings`)) :
```rust
impl Solution {
    pub fn count_days(days: i32, mut meetings: Vec<Vec<i32>>) -> i32 {
        meetings.sort();
        let n: usize = meetings.len();
        let mut maximum: i32 = meetings[0][1];
        let mut result: i32 = meetings[0][0] - 1;
        for index in 1..n {
            if maximum < meetings[index][0] {
                result += meetings[index][0] - maximum - 1;
            }

            if maximum < meetings[index][1] {
                maximum = meetings[index][1];
            }
        }

        if maximum < days {
            result += days - maximum;
        }

        return result
    }
}
```
