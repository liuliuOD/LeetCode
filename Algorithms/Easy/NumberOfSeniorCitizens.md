![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2678. [Number Of Senior Citizens](https://leetcode.com/problems/number-of-senior-citizens)

### Solution :

Method 1 (In biweekly contest 104) :
```rust
impl Solution {
    pub fn count_seniors(details: Vec<String>) -> i32 {
        let mut result = 0;
        for detail in details {
            let mut tt = detail.chars().rev();
            tt.next();
            tt.next();
            if tt.next().unwrap().to_digit(10).unwrap() + 10 * tt.next().unwrap().to_digit(10).unwrap() > 60 {
                result += 1;
            }
        }
        result as i32
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `details`)) :
```rust
impl Solution {
    pub fn count_seniors(details: Vec<String>) -> i32 {
        let mut result: i32 = 0;
        for person in details {
            if (person.as_bytes()[11] == b'6' && person.as_bytes()[12] > b'0') || (person.as_bytes()[11] > b'6') {
                result += 1;
            }
        }

        return result
    }
}
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `details`)) :
```rust
impl Solution {
    pub fn count_seniors(details: Vec<String>) -> i32 {
        let mut result: i32 = 0;
        for person in details {
            let age: u8 = *(&person[11..=12].parse::<u8>().unwrap());
            if age > 60 {
                result += 1;
            }
        }

        return result
    }
}
```

Method 4 (One-Line, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `details`)) :
```rust
impl Solution {
    pub fn count_seniors(details: Vec<String>) -> i32 {
        return details.iter().filter(|person| *(&person[11..=12].parse::<u8>().unwrap()) > 60).count() as _
    }
}
```
