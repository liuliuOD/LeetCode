## [Add Digits](https://leetcode.com/problems/add-digits)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn add_digits(mut num: i32) -> i32 {
        let mut sum = num % 10;
        while num / 10 > 0 {
            num = num / 10;
            sum += num % 10;

            if sum / 10 > 0 && num < 10 {
                num = sum;
                sum = num % 10;
            }
        }

        sum
    }
}
```

Method 2 (time complexity: O(1)) :
```rust
impl Solution {
    pub fn add_digits(mut num: i32) -> i32 {
        match num {
            0 => 0,
            _ => {
                match num % 9 {
                    0 => 9,
                    remainder => remainder,
                }
            }
        }
    }
}
```
