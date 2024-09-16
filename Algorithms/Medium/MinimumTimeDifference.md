![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 539. [Minimum Time Difference](https://leetcode.com/problems/minimum-time-difference)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `time_points`)) :
```rust
const BASE: u8 = b'0';
const MINUTES_MAXIMUM: i32 = 24 * 60;

impl Solution {
    pub fn find_min_difference(mut time_points: Vec<String>) -> i32 {
        let n: usize = time_points.len();
        time_points.sort();
        let mut result: i32 = MINUTES_MAXIMUM;
        for index in 0..n {
            let minutes_current: i32 = Self::get_minutes(&time_points[index]);
            let mut minutes_previous: i32 = match index {
                0 => Self::get_minutes(&time_points[n-1]),
                _ => Self::get_minutes(&time_points[index-1]),
            };
            result = *vec![result, MINUTES_MAXIMUM-minutes_current+minutes_previous, MINUTES_MAXIMUM-minutes_previous+minutes_current, (minutes_current-minutes_previous).abs()].iter().min().unwrap();
        }

        return result
    }

    fn get_minutes(item: &String) -> i32 {
        let bytes = item.as_bytes();
        return (
            (bytes[0]-BASE) as i32 *10 + (bytes[1]-BASE) as i32
            )*60 + (bytes[3]-BASE) as i32 *10 + (bytes[4]-BASE) as i32
    }
}
```

Method 2 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `time_points`)) :
```rust
const BASE: u8 = b'0';
const MINUTES_MAXIMUM: i32 = 24 * 60;

impl Solution {
    pub fn find_min_difference(mut time_points: Vec<String>) -> i32 {
        let n: usize = time_points.len();
        time_points.sort();
        let mut result: i32 = MINUTES_MAXIMUM;
        let mut times: Vec<i32> = vec![i32::MAX; n];
        for index in 0..n {
            let minutes_current: i32 = Self::get_minutes(&time_points[index]);
            let index_previous: usize = match index {
                0 => n-1,
                _ => index-1,
            };
            let mut minutes_previous: i32 = match times[index_previous] == i32::MAX {
                true => {
                    times[index_previous] = Self::get_minutes(&time_points[index_previous]);

                    times[index_previous]
                },
                _ => {
                    times[index_previous]
                }
            };
            result = *vec![result, MINUTES_MAXIMUM-minutes_current+minutes_previous, MINUTES_MAXIMUM-minutes_previous+minutes_current, (minutes_current-minutes_previous).abs()].iter().min().unwrap();
        }

        return result
    }

    fn get_minutes(item: &String) -> i32 {
        return item[0..=1].parse::<i32>().unwrap()*60 + item[3..=4].parse::<i32>().unwrap()
    }
}
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `time_points`)) :
```rust
const BASE: u8 = b'0';
const MINUTES_MAXIMUM: i32 = 24 * 60;

impl Solution {
    pub fn find_min_difference(time_points: Vec<String>) -> i32 {
        let n: usize = time_points.len();
        let mut minutes: Vec<bool> = vec![false; MINUTES_MAXIMUM as usize];
        for index in 0..n {
            let minute: usize = Self::get_minutes(&time_points[index]) as usize;
            if minutes[minute] {
                return 0
            }

            minutes[minute] = true;
        }

        let mut minutes_first: i32 = i32::MAX;
        let mut minutes_previous: i32 = i32::MAX;
        let mut result: i32 = MINUTES_MAXIMUM;
        for minute in 0..MINUTES_MAXIMUM {
            if minutes[minute as usize] == false {
                continue;
            }

            if minutes_first == i32::MAX {
                minutes_first = minute;
            }

            if minutes_previous != i32::MAX {
                result = i32::min(result, minute - minutes_previous);
            }

            minutes_previous = minute;
        }

        return i32::min(result, MINUTES_MAXIMUM-minutes_previous+minutes_first)
    }

    fn get_minutes(item: &String) -> i32 {
        return item[0..=1].parse::<i32>().unwrap()*60 + item[3..=4].parse::<i32>().unwrap()
    }
}
```
