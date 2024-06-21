![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1052. [Grumpy Bookstore Owner](https://leetcode.com/problems/grumpy-bookstore-owner)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(N)$ (N: length of `customers`), Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn max_satisfied(customers: Vec<i32>, grumpy: Vec<i32>, minutes: i32) -> i32 {
        let mut result: i32 = 0;
        let mut customer_in_grumpy: i32 = 0;
        let mut maximum: i32 = 0;
        for index in 0..customers.len() {
            match grumpy[index] {
                0 => result += customers[index],
                1 | _ => customer_in_grumpy += customers[index],
            };

            if index as i32 >= minutes && grumpy[index-minutes as usize] == 1 {
                customer_in_grumpy -= customers[index-minutes as usize];
            }

            if customer_in_grumpy > maximum {
                maximum = customer_in_grumpy;
            }
        }

        return result + maximum
    }
}
```

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(N)$ (N: length of `customers`), Space Complexity: $O(1)$) :
```python
class Solution:
    def maxSatisfied(self, customers: List[int], grumpy: List[int], minutes: int) -> int:
        cumulative = 0
        maximum = 0
        result = 0
        for index in range(len(customers)):
            if grumpy[index] == 1:
                cumulative += customers[index]
            else:
                result += customers[index]

            if index >= minutes and grumpy[index-minutes] == 1:
                cumulative -= customers[index-minutes]

            maximum = max(maximum, cumulative)

        return result + maximum
```
