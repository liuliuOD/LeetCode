![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Find The Longest Valid Obstacle Course At Each Position](https://leetcode.com/problems/find-the-longest-valid-obstacle-course-at-each-position)

### Solution :

Method 1 (left to right search) :
```rust
impl Solution {
    pub fn longest_obstacle_course_at_each_position(obstacles: Vec<i32>) -> Vec<i32> {
        let mut current_ordered = vec![obstacles[0]];
        let mut result = vec![1];
        for index in 1..obstacles.len() {
            if current_ordered[current_ordered.len() - 1] <= obstacles[index] {
                current_ordered.push(obstacles[index]);
                result.push(current_ordered.len() as i32);
                continue;
            }

            for (index_ordered, &item_ordered) in current_ordered.iter().enumerate() {
                if item_ordered > obstacles[index] {
                    current_ordered[index_ordered] = obstacles[index];
                    result.push((index_ordered + 1) as i32);
                    break;
                }
            }
        }

        result
    }
}
```

Method 2 (Binary search) :
```rust
impl Solution {
    pub fn longest_obstacle_course_at_each_position(obstacles: Vec<i32>) -> Vec<i32> {
        let mut current_ordered = vec![obstacles[0]];
        let mut result = vec![1];

        for index in 1..obstacles.len() {
            if current_ordered[current_ordered.len() - 1] <= obstacles[index] {
                current_ordered.push(obstacles[index]);
                result.push(current_ordered.len() as i32);
                continue;
            }

            let obstacle = obstacles[index];
            let index_current = Self::binary_search(&current_ordered, obstacle);
            current_ordered[index_current] = obstacle;
            result.push((index_current+1) as i32);
        }

        result
    }

    fn binary_search(nums: &Vec<i32>, target: i32) -> usize {
        let n = nums.len();
        let mut left = 0;
        let mut right = n;
        while left < right {
            let middle = left + (right - left) / 2;

            if nums[middle] <= target {
                left = middle + 1;
            } else {
                right = middle;
            }
        }

        left
    }
}
```
