![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3011. [Find If Array Can Be Sorted](https://leetcode.com/problems/find-if-array-can-be-sorted)

### Solution :

Method 1 (Bubble Sort, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn can_sort_array(mut nums: Vec<i32>) -> bool {
        let n: usize = nums.len();
        let mut amount_bit_one: u32 = nums[0].count_ones();
        let mut minimum: i32 = i32::MAX;
        let mut maximum: i32 = i32::MIN;
        let mut index_start: usize = 0;
        for index in 1..n {
            if nums[index].count_ones() != amount_bit_one {
                Self::sort(index_start, index-1, &mut nums);
                if !Self::valid(maximum, nums[index_start], nums[index]) {
                    return false
                }

                minimum = nums[index_start];
                maximum = nums[index-1];
                index_start = index;
                amount_bit_one = nums[index].count_ones();
            }
        }

        Self::sort(index_start, n-1, &mut nums);
        return Self::valid(maximum, nums[index_start], nums[n-1])
    }

    fn sort(index_start: usize, index_end: usize, nums: &mut Vec<i32>) {
        for index_left in index_start..index_end {
            for index_right in index_left+1..=index_end {
                if nums[index_left] > nums[index_right] {
                    nums.swap(index_left, index_right);
                }
            }
        }
    }

    fn valid(maximum: i32, minimum_current: i32, maximum_current: i32) -> bool {
        return maximum <= minimum_current
            && minimum_current <= maximum_current
    }
}
```

Method 2 (Bubble Sort, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn can_sort_array(mut nums: Vec<i32>) -> bool {
        let n: usize = nums.len();
        for index in 0..n {
            for index_next in index+1..n {
                if nums[index] <= nums[index_next] {
                    continue;
                }
                else if nums[index].count_ones() != nums[index_next].count_ones() {
                    return false
                }

                nums.swap(index, index_next);
            }
        }

        return true
    }
}
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn can_sort_array(mut nums: Vec<i32>) -> bool {
        let mut minimum: i32 = nums[0];
        let mut maximum: i32 = nums[0];
        let mut maximum_previous: i32 = i32::MIN;
        for index in 1..nums.len() {
            if nums[index].count_ones() == nums[index-1].count_ones() {
                minimum = i32::min(minimum, nums[index]);
                maximum = i32::max(maximum, nums[index]);
            } else if maximum_previous <= minimum {
                maximum_previous = maximum;
                maximum = nums[index];
                minimum = nums[index];
            } else {
                return false
            }
        }

        return maximum_previous <= minimum
    }
}
```
