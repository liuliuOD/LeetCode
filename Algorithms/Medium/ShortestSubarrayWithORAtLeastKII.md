![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 3097. [Shortest Subarray With OR At Least K II](https://leetcode.com/problems/shortest-subarray-with-or-at-least-k-ii)

### Solution :

Method 1 (Prefix Sum + Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the element in `nums`)) :
```rust
const BIT_MAXIMUM: usize = 30;

impl Solution {
    pub fn minimum_subarray_length(nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        let mut prefix_sum: Vec<[i32; 30]> = Vec::with_capacity(n+1);
        prefix_sum.push([0; BIT_MAXIMUM]);
        let mut amount_remove: usize = 0;
        let mut amount_all: usize = 1;
        let mut result: i32 = i32::MAX;
        while amount_all <= n && amount_remove < amount_all {
            if prefix_sum.len() == amount_all {
                prefix_sum.push(prefix_sum[amount_all-1]);

                for bit in 0..BIT_MAXIMUM {
                    if nums[amount_all-1] & 1<<bit > 0 {
                        prefix_sum[amount_all][bit] += 1;
                    }
                }
            }

            let mut or: i32 = 0;
            for bit in 0..BIT_MAXIMUM {
                if prefix_sum[amount_all][bit]-prefix_sum[amount_remove][bit] > 0 {
                    or += 1 << bit;
                }
            }

            if or >= k {
                result = i32::min(result, (amount_all-amount_remove) as i32);
                amount_remove += 1;
            } else {
                amount_all += 1;
            }

        }

        return match result {
            i32::MAX => -1,
            other => other,
        }
    }
}
```

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the element in `nums`)) :
```rust
const BIT_MAXIMUM: usize = 30;

impl Solution {
    pub fn minimum_subarray_length(nums: Vec<i32>, k: i32) -> i32 {
        let n: usize = nums.len();
        let mut prefix_sum: [i32; 30] = [0; BIT_MAXIMUM];
        Self::add_element(0, &nums, &mut prefix_sum);

        let mut amount_remove: usize = 0;
        let mut amount_all: usize = 1;
        let mut result: i32 = i32::MAX;
        while amount_all <= n+1 && amount_remove < amount_all {
            let mut or: i32 = 0;
            for bit in 0..BIT_MAXIMUM {
                if prefix_sum[bit] > 0 {
                    or += 1 << bit;
                }
            }

            if or >= k {
                result = i32::min(result, (amount_all-amount_remove) as i32);

                amount_remove += 1;
                for bit in 0..BIT_MAXIMUM {
                    if nums[amount_remove-1] & 1<<bit > 0 {
                        prefix_sum[bit] -= 1;
                    }
                }
            } else {
                amount_all += 1;

                if amount_all > 1 && amount_all < n+1 {
                    Self::add_element(amount_all-1, &nums, &mut prefix_sum);
                }
            }
        }

        return match result {
            i32::MAX => -1,
            other => other,
        }
    }

    fn add_element(index: usize, nums: &Vec<i32>, prefix_sum: &mut [i32; BIT_MAXIMUM]) {
        for bit in 0..BIT_MAXIMUM {
            if nums[index] & 1<<bit > 0 {
                prefix_sum[bit] += 1;
            }
        }
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the element in `nums`)) :
```java
class Solution {
    public int minimumSubarrayLength(int[] nums, int k) {
        int[] counter = new int[30];
        int result = Integer.MAX_VALUE;
        int amount_remove = 0;
        for (int amount_all=1; amount_all<=nums.length; amount_all++) {
            this.addCounter(counter, nums[amount_all-1]);

            while (amount_remove < amount_all) {
                int or = 0;
                for (int bit=0; bit<30; bit++) {
                    if (counter[bit] > 0) {
                        or |= 1 << bit;
                    }
                }

                if (or >= k) {
                    result = Integer.min(result, amount_all - amount_remove);
                    this.removeCounter(counter, nums[amount_remove]);
                    amount_remove += 1;
                } else {
                    break;
                }
            }

            if (amount_remove >= amount_all) {
                break;
            }
        }

        if (result == Integer.MAX_VALUE)
            return -1;
        return result;
    }

    void addCounter(int[] counter, int num) {
        for (int bit=0; bit<30; bit++) {
            if ((1<<bit & num) > 0) {
                counter[bit] += 1;
            }
        }
    }

    void removeCounter(int[] counter, int num) {
        for (int bit=0; bit<30; bit++) {
            if ((1<<bit & num) > 0) {
                counter[bit] -= 1;
            }
        }
    }
}
```
