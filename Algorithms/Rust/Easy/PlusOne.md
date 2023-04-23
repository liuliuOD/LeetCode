## [Plus One](https://leetcode.com/problems/plus-one)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        let mut result = vec![];
        let mut offset = 1;
        for i in 0..digits.len() {
            let index = digits.len() - i - 1;
            match offset == 1 {
                true => {
                    match digits[index] == 9 {
                        true => {
                            result.push(0);
                            offset = 1;
                        },
                        false => {
                            result.push(digits[index] + 1);
                            offset = 0;
                        }
                    }
                },
                false => {
                    result.push(digits[index]);
                }
            }
        }

        if offset == 1 {
            result.push(1);
        }

        result.reverse();
        result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        let mut result = digits.clone();
        result.reverse();
        let mut iter_position = 0;
        let mut offset = 1;
        while offset == 1 {
            match result.get(iter_position) {
                None => if offset == 1 {
                    result.push(1);
                    offset = 0;
                },
                Some(value) => if offset == 1 {
                    match result[iter_position] == 9 {
                        true => {
                            result[iter_position] = 0;
                            iter_position += 1;
                        },
                        false => {
                            result[iter_position] += 1;
                            offset = 0;
                        }
                    }
                },
            }
        }

        result.reverse();
        result
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        let mut result = digits.clone();
        let mut iter_position = result.len() - 1;
        let mut offset = 1;
        while offset == 1 {
            match result.get(iter_position) {
                None => if offset == 1 {
                    result = [vec![1], result].concat();
                    offset = 0;
                },
                Some(value) => if offset == 1 {
                    match result[iter_position] == 9 {
                        true => {
                            result[iter_position] = 0;
                            iter_position -= 1;
                        },
                        false => {
                            result[iter_position] += 1;
                            offset = 0;
                        }
                    }
                },
            }
        }

        result
    }
}
```

Method 4 :
```rust
impl Solution {
    pub fn plus_one(mut digits: Vec<i32>) -> Vec<i32> {
        for value in digits.iter_mut().rev() {
            let sum = *value + 1;

            *value = sum % 10;
            if sum < 10 {
                return digits;
            }
        }

        [vec![1], digits].concat()
    }
}
```
