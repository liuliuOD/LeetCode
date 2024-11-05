![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2914. [Minimum Number Of Changes To Make Binary String Beautiful](https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 504/577, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_char: Vec<u8> = s.as_bytes().to_vec();
        let mut prefix_sum_one: Vec<i32> = vec![0; n+1];
        for index in 0..n {
            prefix_sum_one[index+1] = prefix_sum_one[index];
            if s_char[index] == b'1' {
                prefix_sum_one[index+1] += 1;
            }
        }

        return i32::min(
            Self::dfs(0, b'0', &s_char, &prefix_sum_one),
            Self::dfs(0, b'1', &s_char, &prefix_sum_one),
        )
    }

    fn dfs(index: usize, element: u8, s_char: &Vec<u8>, prefix_sum_one: &Vec<i32>) -> i32 {
        if index >= s_char.len()-1 {
            return 0
        }

        let mut result: i32 = match element {
            b'0' => prefix_sum_one[index+2] - prefix_sum_one[index],
            b'1' | _ => 2 - (prefix_sum_one[index+2] - prefix_sum_one[index]),
        };

        return result + i32::min(
            Self::dfs(index+2, b'0', s_char, prefix_sum_one),
            Self::dfs(index+2, b'1', s_char, prefix_sum_one),
        )
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_char: Vec<u8> = s.as_bytes().to_vec();
        let mut prefix_sum_one: Vec<i32> = vec![0; n+1];
        for index in 0..n {
            prefix_sum_one[index+1] = prefix_sum_one[index];
            if s_char[index] == b'1' {
                prefix_sum_one[index+1] += 1;
            }
        }

        let mut memoization: HashMap<(usize, u8), i32> = HashMap::new();
        return i32::min(
            Self::dfs(0, b'0', &mut memoization, &s_char, &prefix_sum_one),
            Self::dfs(0, b'1', &mut memoization, &s_char, &prefix_sum_one),
        )
    }

    fn dfs(index: usize, element: u8, memoization: &mut HashMap<(usize, u8), i32>, s_char: &Vec<u8>, prefix_sum_one: &Vec<i32>) -> i32 {
        if index >= s_char.len()-1 {
            return 0
        }

        let key: (usize, u8) = (index, element);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: i32 = match element {
            b'0' => prefix_sum_one[index+2] - prefix_sum_one[index],
            b'1' | _ => 2 - (prefix_sum_one[index+2] - prefix_sum_one[index]),
        };

        result += i32::min(
            Self::dfs(index+2, b'0', memoization, s_char, prefix_sum_one),
            Self::dfs(index+2, b'1', memoization, s_char, prefix_sum_one),
        );

        memoization.entry(key).or_insert(result);
        return result
    }
}
```

Method 3 (Dynamic Programming + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_bytes: Vec<u8> = s.as_bytes().to_vec();
        let mut dp: Vec<i32> = vec![i32::MAX; 2];
        for index in 0..n/2 {
            if index == 0 {
                dp[0] = (s_bytes[index] + s_bytes[index+1] - BASE*2) as i32;
                dp[1] = 2 - (s_bytes[index] + s_bytes[index+1] - BASE*2) as i32;
            } else {
                let mut temp: Vec<i32> = vec![i32::MAX; 2];
                temp[0] = (s_bytes[index*2] + s_bytes[index*2+1] - BASE*2) as i32 + dp.iter().min().unwrap();
                temp[1] = 2 - (s_bytes[index*2] + s_bytes[index*2+1] - BASE*2) as i32 + dp.iter().min().unwrap();
                dp = temp;
            }
        }

        return *dp.iter().min().unwrap()
    }
}
```

Method 4 (Dynamic Programming + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_bytes: Vec<u8> = s.as_bytes().to_vec();
        let mut dp: [i32; 2] = [i32::MAX; 2];
        for index in 0..n/2 {
            let mut temp: [i32; 2] = [i32::MAX; 2];
            temp[0] = (s_bytes[index*2] + s_bytes[index*2+1] - BASE*2) as i32;
            temp[1] = 2 - (s_bytes[index*2] + s_bytes[index*2+1] - BASE*2) as i32;
            if index > 0 {
                temp[0] += *dp.iter().min().unwrap();
                temp[1] += *dp.iter().min().unwrap();
            }

            dp = temp;
        }

        return *dp.iter().min().unwrap()
    }
}
```

Method 4 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let s_char: Vec<char> = s.chars().collect();
        return (0..s.len()).step_by(2)
            .map(|index| {
                return match s_char[index] == s_char[index+1] {
                    true => 0,
                    false => 1,
                }
            })
            .sum()
    }
}
```

Method 5 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_changes(s: String) -> i32 {
        return s.as_bytes()
            .chunks_exact(2)
            .filter(|items| items[0] != items[1])
            .count() as _
    }
}
```

### Solution :

Method 1 (Greedy + Stream API, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```java
class Solution {
    public int minChanges(String s) {
        return (int) IntStream.range(0, s.length()/2)
            .filter(index -> s.charAt(index*2) != s.charAt(index*2+1))
            .count();
    }
}
```

Method 2 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```java
class Solution {
    public int minChanges(String s) {
        int result = 0;
        /* Option 1 */
        for (int index=0; index<s.length()/2; index++) {
            if (s.charAt(index*2) != s.charAt(index*2+1)) {
        /* Option 2

        for (int index=0; index<s.length(); index+=2) {
            if (s.charAt(index) != s.charAt(index+1)) {
        */
                result++;
            }
        }

        return result;
    }
}
```
