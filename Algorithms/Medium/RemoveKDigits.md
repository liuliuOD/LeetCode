![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Remove K Digits](https://leetcode.com/problems/remove-k-digits)

### Solution :

Method 1 (Monotonic Stack) :
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
