![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2563. [Count The Number Of Fair Pairs](https://leetcode.com/problems/count-the-number-of-fair-pairs)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 48/54, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_fair_pairs(nums: Vec<i32>, lower: i32, upper: i32) -> i64 {
        let n: usize = nums.len();
        let mut result: i64 = 0;
        for index_i in 0..n {
            for index_j in index_i+1..n {
                let sum: i32 = nums[index_i] + nums[index_j];
                if lower <= sum && sum <= upper {
                    result += 1;
                }
            }
        }

        return result
    }
}
```

Method 2 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn count_fair_pairs(mut nums: Vec<i32>, lower: i32, upper: i32) -> i64 {
        if nums.len() <= 1 {
            return 0
        }

        nums.sort();

        return Self::amount_pairs(&nums, upper+1) - Self::amount_pairs(&nums, lower)
    }

    fn amount_pairs(nums: &Vec<i32>, upper: i32) -> i64 {
        let mut index_left: usize = 0;
        let mut index_right: usize = nums.len() - 1;
        let mut result: i64 = 0;
        while index_left < index_right {
            if nums[index_left]+nums[index_right] < upper {
                result += (index_right - index_left) as i64;
                index_left += 1;
                continue;
            }

            if index_right == 0 {
                break;
            }
            index_right -= 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```java
class Solution {
    public long countFairPairs(int[] nums, int lower, int upper) {
        Arrays.sort(nums);

        return this.amountPairs(nums, upper+1) - this.amountPairs(nums, lower);
    }

    long amountPairs(int[] nums, int upper) {
        long result = 0;
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            if (nums[left]+nums[right] < upper) {
                result += right - left;
                left += 1;
                continue;
            }

            right -= 1;
        }

        return result;
    }
}
```
