![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 402. [Remove K Digits](https://leetcode.com/problems/remove-k-digits)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn remove_kdigits(num: String, k: i32) -> String {
        let mut k = k as usize;
        let mut stack:Vec<char> = vec![];
        for character in num.chars().into_iter() {
            while !stack.is_empty() && k > 0 && *stack.last().unwrap() > character {
                stack.pop();
                k -= 1;
            }

            // return won't includes '0' if at leading position
            if character != '0' || !stack.is_empty() {
                stack.push(character);
            }
        }        

        // pop out until remove times have been completed
        while k > 0 && stack.len() > 0 {
            stack.pop();
            k -= 1;
        }
        
        match stack.len() > 0 {
            false => String::from("0"),
            true => stack.iter().collect::<String>(),
        }
    }
}
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        for digit in num:
            digit: int = int(digit)
            while k and stack and stack[-1] > digit:
                k -= 1
                stack.pop()

            if stack or digit > 0:
                stack.append(digit)

        while k and stack:
            k -= 1
            stack.pop()

        return ''.join([str(digit) for digit in stack]) if stack else "0"
```

Method 2 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        for digit in num:
            while k and stack and stack[-1] > digit:
                k -= 1
                stack.pop()

            if stack or digit is not "0":
                stack.append(digit)

        while k and stack:
            k -= 1
            stack.pop()

        return ''.join(stack) if stack else "0"
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```go
func removeKdigits(num string, k int) string {
    var result string
    for _, char := range num {
        for k > 0 && len(result) > 0 && result[len(result)-1] > byte(char) {
            k--
            result = result[:len(result)-1]
        }

        if len(result) > 0 || char != '0' {
            result += string(char)
        }
    }

    if k > 0 {
        if len(result) < k {
            return "0"
        }

        result = result[:len(result)-k]
    }

    if len(result) > 0 {
        return result
    }
    return "0"
}
```

Method 2 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func removeKdigits(num string, k int) string {
    var result []rune
    for _, char := range num {
        for k > 0 && len(result) > 0 && result[len(result)-1] > char {
            k--
            result = result[:len(result)-1]
        }

        if len(result) > 0 || char != '0' {
            result = append(result, char)
        }
    }

    if len(result) == 0 {
        return "0"
    }

    if k > 0 {
        if len(result) <= k {
            return "0"
        }

        result = result[:len(result)-k]
    }

    return string(result)
}
```
