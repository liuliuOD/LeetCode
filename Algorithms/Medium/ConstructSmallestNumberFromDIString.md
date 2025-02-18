![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2375. [Construct Smallest Number From DI String](https://leetcode.com/problems/construct-smallest-number-from-di-string)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(N!*N^2)$, Space Complexity: $O(N)$ (N: the length of `pattern`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn smallest_number(pattern: String) -> String {
        let n: usize = pattern.len();
        let pattern: Vec<char> = pattern.chars().into_iter().collect::<Vec<char>>();
        let mut visited: [bool; 10] = [false; 10];
        let mut candidates: Vec<String> = Vec::new();

        for digit in 1..=9 {
            let mut num: Vec<u8> = Vec::from([BASE+digit]);
            visited[digit as usize] = true;
            Self::backtracking(0, &mut num, &mut visited, &mut candidates, &pattern);
            visited[digit as usize] = false;
        }

        candidates.sort();
        return (*candidates[0]).to_string()
    }

    fn backtracking(index: usize, num: &mut Vec<u8>, visited: &mut [bool; 10], candidates: &mut Vec<String>, pattern: &Vec<char>) {
        let n: usize = pattern.len();
        if index >= n {
            candidates.push(String::from_utf8(num.clone()).unwrap());
            return
        }

        let previous: u8 = *num.last().unwrap();
        for offset in 1..=9 {
            if visited[offset] {
                continue;
            }

            let next: u8 = BASE + offset as u8;
            match pattern[index] {
                'I' => {
                    if previous >= next {
                        continue;
                    }
                },
                _ => {
                    if previous <= next {
                        continue;
                    }
                },
            };
            visited[offset] = true;
            num.push(next);
            Self::backtracking(index+1, num, visited, candidates, pattern);
            num.pop();
            visited[offset] = false;
        }
    }
}
```

Method 2 (Backtracking + Early Return, Time Complexity: $O(N!*N^2)$, Space Complexity: $O(N)$ (N: the length of `pattern`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn smallest_number(pattern: String) -> String {
        let n: usize = pattern.len();
        let pattern: Vec<char> = pattern.chars().into_iter().collect::<Vec<char>>();
        let mut visited: [bool; 10] = [false; 10];
        let mut candidates: Vec<String> = Vec::new();

        for digit in 1..=9 {
            let mut num: Vec<u8> = Vec::from([BASE+digit]);
            visited[digit as usize] = true;
            Self::backtracking(0, &mut num, &mut visited, &mut candidates, &pattern);
            if candidates.len() > 0 {
                return (*candidates[0]).to_string()
            }

            visited[digit as usize] = false;
        }

        return (*candidates[0]).to_string()
    }

    fn backtracking(index: usize, num: &mut Vec<u8>, visited: &mut [bool; 10], candidates: &mut Vec<String>, pattern: &Vec<char>) {
        let n: usize = pattern.len();
        if index >= n {
            candidates.push(String::from_utf8(num.clone()).unwrap());
            return
        }

        let previous: u8 = *num.last().unwrap();
        for offset in 1..=9 {
            if visited[offset] {
                continue;
            }

            let next: u8 = BASE + offset as u8;
            match pattern[index] {
                'I' => {
                    if previous >= next {
                        continue;
                    }
                },
                _ => {
                    if previous <= next {
                        continue;
                    }
                },
            };
            visited[offset] = true;
            num.push(next);
            Self::backtracking(index+1, num, visited, candidates, pattern);
            num.pop();
            visited[offset] = false;
        }
    }
}
```

Method 3 (Greedy, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the length of `pattern`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn smallest_number(pattern: String) -> String {
        let n: usize = pattern.len();
        let pattern: Vec<char> = pattern.chars().into_iter().collect::<Vec<char>>();
        let mut result: Vec<u8> = Vec::new();
        let mut index_previous: usize = 0;
        for index in 0..n+1 {
            result.push(BASE+index as u8+1);

            if index == n || pattern[index] == 'I' {
                result[index_previous..=index].reverse();
                index_previous = index + 1;
            }
        }

        return String::from_utf8(result).unwrap()
    }
}
```
