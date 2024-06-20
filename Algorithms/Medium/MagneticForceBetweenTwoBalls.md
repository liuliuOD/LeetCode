![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1552. [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(N))$ (N: length of `position`), Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn max_distance(mut position: Vec<i32>, m: i32) -> i32 {
        position.sort();
        let mut left: i32 = 0;
        let mut right: i32 = *position.iter().max().unwrap() - *position.iter().min().unwrap();
        while left <= right {
            let distance: i32 = left + (right - left) / 2;
            let mut index_previous: usize = 0;
            let mut m_current: i32 = 1;
            for (index, &p) in position.iter().enumerate() {
                if p - position[index_previous] >= distance {
                    index_previous = index;
                    m_current += 1;
                }

                if m_current == m {
                    break;
                }
            }

            if m_current < m {
                right = distance - 1;
            } else {
                left = distance + 1;
            }
        }

        return right
    }
}
```

Method 2 (Binary Search + Speed Up, Time Complexity: $O(N*Log(N))$ (N: length of `position`), Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn max_distance(mut position: Vec<i32>, m: i32) -> i32 {
        position.sort_unstable();
        let mut left: i32 = 1;
        let mut right: i32 = (*position.last().unwrap() - position[0]) / (m - 1);
        while left <= right {
            let distance: i32 = left + (right - left) / 2;
            let mut index_previous: usize = 0;
            let mut m_current: i32 = 1;
            for (index, &p) in position.iter().enumerate() {
                if p - position[index_previous] >= distance {
                    index_previous = index;
                    m_current += 1;
                }

                if m_current == m {
                    break;
                }
            }

            if m_current < m {
                right = distance - 1;
            } else {
                left = distance + 1;
            }
        }

        return right
    }
}
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(N))$ (N: length of `position`), Space Complexity: $O(N)$) :
```python
class Solution:
    def maxDistance(self, position: List[int], m: int) -> int:
        position.sort()
        left, right = 0, max(position) - min(position)
        while left <= right:
            distance = left + (right - left)//2

            position_previous = -inf
            m_temp = m
            for position_current in position:
                if position_current - position_previous >= distance:
                    m_temp -= 1
                    position_previous = position_current

                if m_temp == 0:
                    break

            if m_temp == 0:
                left = distance + 1
            else:
                right = distance - 1

        return right
```
