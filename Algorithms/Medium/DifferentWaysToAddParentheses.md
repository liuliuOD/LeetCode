![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 241. [Different Ways To Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses)

### Solution :

Method 1 (Time Complexity: $O(N*2^N)$, Space Complexity: $O(2^N)$ (N: the length of `expression`)) :
```rust
impl Solution {
    pub fn diff_ways_to_compute(expression: String) -> Vec<i32> {
        if expression.len() == 0 {
            return Vec::new()
        } else if expression.len() == 1 || (expression.len() == 2 && expression.parse::<i32>().is_ok()) {
            return Vec::from([expression.parse::<i32>().unwrap()])
        }

        let expression_bytes = expression.as_bytes();
        let n: usize = expression_bytes.len();
        let mut result: Vec<i32> = Vec::new();
        for index in 0..n {
            if b'0' <= expression_bytes[index] && expression_bytes[index] <= b'9' {
                continue;
            }

            let values_left: Vec<i32> = Self::diff_ways_to_compute(String::from_utf8(expression_bytes[0..index].to_vec()).unwrap());
            let mut values_right: Vec<i32> = Vec::new();
            if index < n-1 {
                values_right = Self::diff_ways_to_compute(String::from_utf8(expression_bytes[index+1..].to_vec()).unwrap());
            }

            for left in values_left.into_iter() {
                for &right in values_right.iter() {
                    match expression_bytes[index] {
                        b'+' => result.push(left + right),
                        b'-' => result.push(left - right),
                        b'*' => result.push(left * right),
                        b'/' => result.push(left / right),
                        _ => {},
                    }
                }
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the element in `nums`)) :
```python
class Solution:
    def diffWaysToCompute(self, expression: str) -> List[int]:
        if len(expression) == 0:
            return []
        elif len(expression) == 1:
            return [int(expression[0])]
        elif len(expression) == 2 and expression[0].isdigit():
            return [int(expression)]

        result = []
        for index, char in enumerate(expression):
            if char.isdigit():
                continue

            result_left = self.diffWaysToCompute(expression[:index])
            result_right = self.diffWaysToCompute(expression[index+1:])
            for left in result_left:
                for right in result_right:
                    match char:
                        case '+':
                            result.append(left + right)
                        case '-':
                            result.append(left - right)
                        case '*':
                            result.append(left * right)
                        case '/':
                            result.append(left // right)

        return result
```
