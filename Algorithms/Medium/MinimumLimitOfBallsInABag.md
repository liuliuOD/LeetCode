![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1760. [Minimum Limit Of Balls In A Bag](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag)

### Solution :

Method 1 (Binary Search, ERROR: "Time Limit Exceeded", 48/58, Time Complexity: $O(N*Log(M)*P)$, Space Complexity: $O(1)$ (M: the maximum element in `nums`, N: the number of the elements in `nums`, P: the average times of each element in `nums` that divided by `max_operations`)):
```rust
impl Solution {
    pub fn minimum_size(nums: Vec<i32>, max_operations: i32) -> i32 {
        let mut left: i32 = 1;
        let mut right: i32 = *nums.iter().max().unwrap();
        while left <= right {
            let middle: i32 = left + (right-left)/2;
            let mut count: i32 = 0;
            for &num in nums.iter() {
                let mut temp = num;
                while temp > middle {
                    temp -= middle;
                    count += 1;
                }
            }

            if count <= max_operations {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return left
    }
}
```

Method 2 (Binary Search, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(1)$ (M: the maximum element in `nums`, N: the number of the elements in `nums`):
```rust
impl Solution {
    pub fn minimum_size(nums: Vec<i32>, max_operations: i32) -> i32 {
        let mut left: i32 = 1;
        let mut right: i32 = *nums.iter().max().unwrap();
        while left <= right {
            let middle: i32 = left + (right-left)/2;
            let mut count: i32 = 0;
            for &num in nums.iter() {
                count += num / middle;
                if num % middle == 0 {
                    count -= 1;
                }
            }

            if count <= max_operations {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return left
    }
}
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(1)$ (M: the maximum element in `nums`, N: the number of the elements in `nums`):
```java
class Solution {
    public int minimumSize(int[] nums, int maxOperations) {
        int left = 1;
        int right = IntStream.of(nums)
                            .max()
                            .orElseThrow(() -> new IllegalArgumentException("Array must not be empty"));
        while (left <= right) {
            int middle = left + (right-left)/2;
            int count = 0;
            for (int num: nums) {
                count += num / middle;
                if (num % middle == 0) {
                    count--;
                }
            }

            if (count <= maxOperations) {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return left;
    }
}
```

Method 2 (Binary Search, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(1)$ (M: the maximum element in `nums`, N: the number of the elements in `nums`):
```java
class Solution {
    public int minimumSize(int[] nums, int maxOperations) {
        int left = 1;
        int right = 0;
        for (int num: nums) {
            right = Math.max(right, num);
        }
        while (left <= right) {
            int middle = left + (right-left)/2;
            int count = 0;
            for (int num: nums) {
                count += (num-1) / middle;
            }

            if (count <= maxOperations) {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return left;
    }
}
```
