## [Maximum Number Of Vowels In A Substring Of Given Length](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length)

### Solution :

Method 1 (precalculate positions of vowels to reduce target amount) :
```rust
use std::cmp;
impl Solution {
    pub fn max_vowels(s: String, k: i32) -> i32 {
        let mut vowels = vec![];
        for (index, ch) in s.chars().into_iter().enumerate() {
            match ch {
                'a' | 'e' | 'i' | 'o' | 'u' => vowels.push(index),
                _ => (),
            };
        }

        vowels.sort();

        let k = k as usize;
        let mut result:i32 = 0;
        for i in 0..vowels.len() {
            let mut temp: i32 = 1;
            let mut counter: usize = i + 1;
            while counter < vowels.len() && vowels[i]+k-1 >= vowels[counter] {
                temp += 1;
                counter += 1;
            }

            result = cmp::max(result, temp);
        }

        result
    }
}
```

Method 2 (Sliding Window) :
```rust
use std::cmp;
impl Solution {
    pub fn max_vowels(s: String, k: i32) -> i32 {
        let k = k as usize;
        let mut result: i32 = 0;
        let mut count: i32 = 0;
        let mut vowels: Vec<char> = vec!['a', 'e', 'i', 'o', 'u'];
        let chars: Vec<char> = s.chars().collect();
        for index in 0..chars.len() {
            if index >= k && vowels.contains(&chars[index-k]) {
                count -= 1;
            }
            if vowels.contains(&chars[index]) {
                count += 1;
            }
            result = cmp::max(result, count);
        }

        result
    }
}
```

Method 3 (Brute Force, ERROR: "Time Limit Exceeded") :
```rust
use std::cmp;
impl Solution {
    pub fn max_vowels(s: String, k: i32) -> i32 {
        let k = k as usize;
        let mut result = 0;
        for i in 0..s.len()-k+1 {
            let mut cal = 0;
            let mut temp = 0;
            while cal < k {
                match &s[i+cal..i+cal+1] {
                    "a" | "e" | "i" | "o" | "u" => temp += 1,
                    _ => (),
                };
                cal += 1;
            }

            result = cmp::max(result, temp);
            if result == k {
                break;
            }
        }

        result as _
    }
}
```
