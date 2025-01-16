![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2425. [Bitwise XOR Of All Pairings](https://leetcode.com/problems/bitwise-xor-of-all-pairings)

### Solution :

Method 1 (XOR, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `nums1`, N: the number of the elements in `nums2`)) :
```rust
impl Solution {
    pub fn xor_all_nums(nums1: Vec<i32>, nums2: Vec<i32>) -> i32 {
        let m: usize = nums1.len();
        let n: usize = nums2.len();
        let mut result: i32 = 0;
        if m % 2 == 1 {
            result = nums2.iter().fold(result, |cumulative, num| cumulative ^ num);
        }
        if n % 2 == 1 {
            result = nums1.iter().fold(result, |cumulative, num| cumulative ^ num);
        }

        return result
    }
}
```

### Solution :

Method 1 (XOR, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `nums1`, N: the number of the elements in `nums2`)) :
```java
class Solution {
    public int xorAllNums(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        int result = 0;
        if (m % 2 == 1) {
            for (int num : nums2) {
                result ^= num;
            }
        }
        if (n % 2 == 1) {
            for (int num : nums1) {
                result ^= num;
            }
        }

        return result;
    }
}
```
