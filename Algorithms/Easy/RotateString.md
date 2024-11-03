![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 796. [Rotate String](https://leetcode.com/problems/rotate-string)

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s` or `goal`)) :
```Rust
impl Solution {
    pub fn rotate_string(mut s: String, goal: String) -> bool {
        let m: usize = s.len();
        let n: usize = goal.len();
        if m != n {
            return false
        }

        s += &s.to_string();
        return s.contains(&goal)
    }
}
```

Method 2 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s` or `goal`)) :
```rust
impl Solution {
    pub fn rotate_string(s: String, goal: String) -> bool {
        return s.len() == goal.len() && (s.clone() + &s.clone()).contains(&goal)
    }
}
```

### Solution :

Method 1 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s` or `goal`)) :
```java
class Solution {
    public boolean rotateString(String s, String goal) {
        return (s.length() == goal.length())
            && s.concat(s).contains(goal);
    }
}
```
