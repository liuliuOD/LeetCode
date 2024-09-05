![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2028. [Find Missing Observations](https://leetcode.com/problems/find-missing-observations)

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `rolls`, N: the value of `n`)) :
```rust
impl Solution {
    pub fn missing_rolls(rolls: Vec<i32>, mean: i32, n: i32) -> Vec<i32> {
        let k: i32 = rolls.len() as i32 + n;
        let mut amount_remaining: i32 = mean*k - rolls.iter().sum::<i32>();

        let mut result: Vec<i32> = Vec::new();
        if amount_remaining > n*6 || amount_remaining < n {
            return result
        }

        let average: i32 = amount_remaining / n;
        /* Option 1 */
        for _ in 0..n {
            result.push(average);
            amount_remaining -= average;
        }
        /* Option 2

        amount_remaining -= average * n;
        result.append(&mut vec![average; n as usize]);
        */
        /* Option 3

        amount_remaining -= average * n;
        result.extend(vec![average; n as usize]);
        */

        let mut index: usize = 0;
        while amount_remaining > 0 {
            if result[index] < 6 {
                let difference: i32 = i32::min(6-result[index], amount_remaining);
                result[index] += difference;
                amount_remaining -= difference;
            }

            index += 1;
        }

        return result
    }
}
```
