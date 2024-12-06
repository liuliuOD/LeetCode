![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2554. [Maximum Number Of Integers To Choose From A Range I](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-i)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `banned`, N: the value of `n`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn max_count(banned: Vec<i32>, n: i32, max_sum: i32) -> i32 {
        let mut set: HashSet<i32> = HashSet::from_iter(banned);
        let mut sum: i64 = 0;
        let mut result: i32 = 0;
        for num in 1..=n {
            if set.contains(&num) {
                continue;
            }

            sum += num as i64;
            result += 1;
            /* Option 1 */
            if sum > max_sum as i64 {
                result -= 1;
                break;
            } else if sum == max_sum as i64 {
                break;
            }
            /* Option 2

            if sum < max_sum as i64 {
                continue;
            }

            if sum > max_sum as i64 {
                result -= 1;
            }
            break;
            */
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `banned`, N: the value of `n`)) :
```java
class Solution {
    public int maxCount(int[] banned, int n, int maxSum) {
        Set<Integer> set = IntStream.of(banned)
                                    .boxed()
                                    .collect(Collectors.toSet());
        int sum = 0;
        int result = 0;
        for (int num=1; num<=n; num++) {
            if (set.contains(num)) {
                continue;
            }

            sum += num;
            result++;
            if (sum < maxSum) {
                continue;
            }

            if (sum > maxSum) {
                result--;
            }
            break;
        }

        return result;
    }
}
```

Method 2 (Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `banned`, N: the value of `n`)) :
```java
class Solution {
    public int maxCount(int[] banned, int n, int maxSum) {
        int sum = 0;
        int result = 0;
        boolean[] invalid = new boolean[10001];
        for (int num: banned) {
            invalid[num] = true;
        }

        for (int num = 1; num<=n; num++) {
            if (sum+num > maxSum) {
                break;
            }

            if (invalid[num]) {
                continue;
            }

            sum += num;
            result++;
        }

        return result;
    }
}
```
