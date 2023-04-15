## [Roman To Integer](https://leetcode.com/problems/roman-to-integer)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn roman_to_int(s: String) -> i32 {
        let hm = HashMap::from([
            ('I', 1),
            ('V', 5),
            ('X', 10),
            ('L', 50),
            ('C', 100),
            ('D', 500),
            ('M', 1000),
        ]);

        let mut result = 0;
        let mut temp = 0;
        for item in s.chars() {
            let mut value = 0;
            match hm.get(&item) {
                Some(&val) => value = val,
                None => {},
            };
            
            if value > temp {
                result -= temp;
            } else {
                result += temp;
            }

            temp = value;
        }

        result += temp;

        result
    }
}
```

Method 2 (use `if let` to replace `match`) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn roman_to_int(s: String) -> i32 {
        let hm = HashMap::from([
            ('I', 1),
            ('V', 5),
            ('X', 10),
            ('L', 50),
            ('C', 100),
            ('D', 500),
            ('M', 1000),
        ]);

        let mut result = 0;
        let mut temp = 0;
        for item in s.chars() {
            let mut value = 0;
            if let Some(&val) = hm.get(&item) {
                value = val;
            };
            
            if value > temp {
                result -= temp;
            } else {
                result += temp;
            }

            temp = value;
        }

        result += temp;

        result
    }
}
```

Method 3 (use `match` to replace `HashMap`) :
```rust
impl Solution {
    pub fn roman_to_int(s: String) -> i32 {
        let mut result = 0;
        let mut temp = 0;
        for item in s.chars() {
            let mut value:i32;

            match item {
                'I' => value = 1,
                'V' => value = 5,
                'X' => value = 10,
                'L' => value = 50,
                'C' => value = 100,
                'D' => value = 500,
                'M' => value = 1000,
                _ => value = 0,
            };
            
            if value > temp {
                result -= temp;
            } else {
                result += temp;
            }

            temp = value;
        }

        result += temp;

        result
    }
}
```

Method 4 :
```rust
impl Solution {
    pub fn roman_to_int(s: String) -> i32 {
        let mut result = 0;
        let mut temp = 0;
        for index in 0..s.len() {
            let value:i32 = Solution::get_integer(&s[index..index+1]);

            if value > temp {
                result -= temp;
            } else {
                result += temp;
            }

            temp = value;
        }

        result += temp;

        result
    }

    fn get_integer(roman: &str) -> i32 {
        match roman {
            "I" => 1,
            "V" => 5,
            "X" => 10,
            "L" => 50,
            "C" => 100,
            "D" => 500,
            "M" => 1000,
            _ => 0,
        }
    }
}
```

Method 5 (remove parameter `temp`) :
```rust
impl Solution {
    pub fn roman_to_int(s: String) -> i32 {
        let mut result = 0;
        let mut value:i32 = 0;
        for index in 0..s.len() {
            value = Solution::get_integer(&s[index..index+1]);

            if (index == s.len() - 1) || (value >= Solution::get_integer(&s[index+1..index+2])) {
                result += value;
            } else {
                result -= value;
            }
        }

        result
    }

    fn get_integer(roman: &str) -> i32 {
        match roman {
            "I" => 1,
            "V" => 5,
            "X" => 10,
            "L" => 50,
            "C" => 100,
            "D" => 500,
            "M" => 1000,
            _ => 0,
        }
    }
}
```
