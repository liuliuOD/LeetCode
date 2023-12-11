![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2961. [Double Modular Exponentiation](https://leetcode.com/problems/double-modular-exponentiation)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn get_good_indices(variables: Vec<Vec<i32>>, target: i32) -> Vec<i32> {
        let mut result: Vec<i32> = vec![];
        for (index, var) in variables.into_iter().enumerate() {
            let a = var[0];
            let mut b = var[1];
            let mut c = var[2];
            let m = var[3];
            let mut a_b: i32 = 1;
            while b > 0 {
                a_b = a_b * a % 10;
                b -= 1;
            }

            let mut a_c: i32 = 1;
            while c > 0 {
                a_c = a_c * a_b % m;
                c -= 1;
            }

            if a_c == target {
                result.push(index as i32);
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (In weekly contest 375, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def getGoodIndices(self, variables: List[List[int]], target: int) -> List[int]:
        result = []
        # Option 1
        for index, var in enumerate(variables):
            a, b, c, m = var
        """
        # Option 2

        for index, (a, b, c, m) in enumerate(variables):
        """
            if pow(pow(a, b, 10), c, m) == target:
                result.append(index)

        return result
```

Method 2 (One-Line) :
```python
class Solution:
    def getGoodIndices(self, variables: List[List[int]], target: int) -> List[int]:
        return [index for index, (a, b, c, m) in enumerate(variables) if pow(pow(a, b, 10), c, m) == target]
```
