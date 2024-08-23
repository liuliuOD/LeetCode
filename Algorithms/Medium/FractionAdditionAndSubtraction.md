![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 592. [Fraction Addition And Subtraction](https://leetcode.com/problems/fraction-addition-and-subtraction)

### Solution :

Method 1 (Simulation, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: length of `expression`)) :
```rust
const BASE: i32 = 2*3*4*5*6*7*8*9*10;

impl Solution {
    pub fn fraction_addition(expression: String) -> String {
        let mut denominators: [i32; 11] = [0; 11];
        let mut numerator: i32 = 0;
        let mut denominator: usize = 0;
        let mut is_positive: bool = true;
        for charactor in expression.into_bytes() {
            if charactor == b'/' {
                numerator = denominator as i32;
                denominator = 0;
            } else if charactor == b'+' {
                if is_positive {
                    denominators[denominator] += numerator;
                } else {
                    denominators[denominator] -= numerator;
                }

                denominator = 0;
                numerator = 0;
                is_positive = true;
            } else if charactor == b'-' {
                if is_positive {
                    denominators[denominator] += numerator;
                } else {
                    denominators[denominator] -= numerator;
                }

                denominator = 0;
                numerator = 0;
                is_positive = false;
            } else {
                let value: usize = (charactor - b'0') as usize;
                denominator = denominator*10 + value;
            }
        }
        if is_positive {
            denominators[denominator] += numerator;
        } else {
            denominators[denominator] -= numerator;
        }

        let mut result_numerator: i32 = 0;
        let mut result_denominator: i32 = BASE;
        for index in 0..=10 {
            let mut numerator: i32 = denominators[index] * BASE;
            if index > 0 {
                numerator /= index as i32;
            }
            result_numerator += numerator;
        }

        let mut factor: i32 = 2;
        while factor <= i32::min(result_numerator.abs(), result_denominator.abs()) {
            if result_numerator%factor == 0 && result_denominator%factor == 0 {
                result_numerator /= factor;
                result_denominator /= factor;
            } else {
                factor += 1;
            }
        }

        if result_numerator == 0 {
            result_denominator = 1;
        }

        return format!("{}/{}", result_numerator, result_denominator)
    }
}
```
