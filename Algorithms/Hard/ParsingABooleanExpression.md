![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1106. [Parsing A Boolean Expression](https://leetcode.com/problems/parsing-a-boolean-expression)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the length of `expression`)) :
```rust
impl Solution {
    pub fn parse_bool_expr(mut expression: String) -> bool {
        while expression.len() > 1 {
            let chars_expression: Vec<char> = expression.chars().collect::<Vec<char>>();
            let n: usize = expression.len();
            let mut should_break: bool = false;
            for index in (0..n).rev() {
                if ['!', '&', '|'].contains(&chars_expression[index]) {
                    should_break = true;
                    for index_end in index+2..n {
                        if chars_expression[index_end] == ')' {
                            expression = expression[0..index].to_string() + &Self::parse(index, index_end, &chars_expression) + &expression[index_end+1..];
                            break;
                        }
                    }
                }

                if should_break {
                    break;
                }
            }
        }

        return match expression.as_str() {
            "t" => true,
            "f" | _ => false,
        }
    }

    fn parse(index_start: usize, index_end: usize, chars_expression: &Vec<char>) -> String {
        return match chars_expression[index_start] {
            '!' => {
                return match chars_expression[index_start+2] {
                    't' => "f".to_string(),
                    'f' | _ => "t".to_string(),
                }
            },
            '&' => {
                for index in index_start+2..index_end {
                    if chars_expression[index] == 'f' {
                        return "f".to_string()
                    }
                }

                return "t".to_string()
            },
            '|' | _ => {
                for index in index_start+2..index_end {
                    if chars_expression[index] == 't' {
                        return "t".to_string()
                    }
                }

                return "f".to_string()
            },
        }
    }
}
```
