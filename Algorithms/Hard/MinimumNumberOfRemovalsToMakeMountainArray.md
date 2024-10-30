![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1671. [Minimum Number Of Removals To Make Mountain Array](https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn minimum_mountain_removals(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut counter_strictly_increment: Vec<i32> = vec![0; n];
        for index in 1..n {
            for index_previous in 0..index {
                if nums[index] > nums[index_previous] {
                    counter_strictly_increment[index] = *[counter_strictly_increment[index], counter_strictly_increment[index_previous] + 1, 2].iter().max().unwrap();
                }
            }
        }

        let mut counter_strictly_decrement: Vec<i32> = vec![0; n];
        for index in (0..n-1).rev() {
            for index_next in index+1..n {
                if nums[index] > nums[index_next] {
                    counter_strictly_decrement[index] = *[counter_strictly_decrement[index], counter_strictly_decrement[index_next] + 1, 2].iter().max().unwrap();
                }
            }
        }

        let mut length_maximum_mountain_array: i32 = 0;
        for index in 1..n-1 {
            if counter_strictly_increment[index] <= 0 || counter_strictly_decrement[index] <= 0 {
                continue;
            }

            length_maximum_mountain_array = i32::max(length_maximum_mountain_array, counter_strictly_increment[index]+counter_strictly_decrement[index]-1);
        }

        return n as i32 - length_maximum_mountain_array
    }
}
```

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```java
class Solution {
    public int minimumMountainRemovals(int[] nums) {
        int n = nums.length;
        int[] increment = new int[n];
        Arrays.fill(increment, 1);
        for (int index=1; index<n; index++) {
            for (int index_previous=0; index_previous<index; index_previous++) {
                if (nums[index_previous] >= nums[index]) {
                    continue;
                }

                increment[index] = Math.max(increment[index], increment[index_previous] + 1);
            }
        }

        int[] decrement = new int[n];
        Arrays.fill(decrement, 1);
        for (int index=n-1; index>=0; index--) {
            for (int index_next=index+1; index_next<n; index_next++) {
                if (nums[index] <= nums[index_next]) {
                    continue;
                }

                decrement[index] = Math.max(decrement[index], decrement[index_next]+1);
            }
        }

        int maximum_mountain_array = 0;
        for (int index=1; index<n-1; index++) {
            if (increment[index] <= 1 || decrement[index] <= 1) {
                continue;
            }

            maximum_mountain_array = Math.max(maximum_mountain_array, increment[index]+decrement[index]-1);
        }

        return n - maximum_mountain_array;
    }
}
```
