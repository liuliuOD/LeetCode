![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1800. [Maximum Ascending Subarray Sum](https://leetcode.com/problems/maximum-ascending-subarray-sum)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of elements in `nums`)) :
```Rust
impl Solution {
    pub fn max_ascending_sum(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut sum: i32 = nums[0];
        let mut result: i32 = sum;
        for index in 0..n-1 {
            /* Option 1 */
            if nums[index] < nums[index+1] {
                sum += nums[index+1];
            } else {
                sum = nums[index+1];
            }
            /* Option 2

            if nums[index] >= nums[index+1] {
                sum = 0;
            }
            sum += nums[index+1];
            */

            result = i32::max(result, sum);
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of elements in `nums`)) :
```java
class Solution {
    public int maxAscendingSum(int[] nums) {
        Iterator<Integer> iterator = Arrays.stream(nums).iterator();
        int sum = iterator.next();
        int result = sum;
        /* Option 1 */
        for(int previous=sum; iterator.hasNext();) {
            int num = iterator.next();
            if (previous >= num) {
                sum = 0;
            }
            sum += num;
            result = Math.max(result, sum);

            previous = num;
        }
        /* Option 2

        for(int previous=sum, num=0; iterator.hasNext(); previous=num) {
            num = iterator.next();
            if (previous >= num) {
                sum = 0;
            }
            sum += num;
            result = Math.max(result, sum);
        }
        */

        return result;
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of elements in `nums`)) :
```java
class Solution {
    public int maxAscendingSum(int[] nums) {
        int n = nums.length;
        int sum = nums[0];
        int result = sum;
        for(int index=0; index<n-1; index++) {
            if (nums[index] >= nums[index+1]) {
                sum = 0;
            }
            sum += nums[index+1];
            result = Math.max(result, sum);
        }

        return result;
    }
}
```
