![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1092. [Shortest Common Supersequence](https://leetcode.com/problems/shortest-common-supersequence)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 16/49, Time Complexity: $O(2^(M+N)*(M+N))$, Space Complexity: $O(2^(M+N)*(M+N))$ (M: the length of `str1`, N: the length of `str2`)) :
```rust
impl Solution {
    pub fn shortest_common_supersequence(str1: String, str2: String) -> String {
        let str1_bytes: &[u8] = str1.as_bytes();
        let str2_bytes: &[u8] = str2.as_bytes();
        let mut result: Vec<String> = Vec::new();
        Self::dfs(0, 0, String::new(), &mut result, str1_bytes, str2_bytes);
        result.sort_by_key(|element| element.len());

        return result[0].clone()
    }

    fn dfs(index1: usize, index2: usize, current: String, result: &mut Vec<String>, str1_bytes: &[u8], str2_bytes: &[u8]) {
        let m: usize = str1_bytes.len();
        let n: usize = str2_bytes.len();
        if index1 >= m && index2 >= n {
            result.push(current);
            return
        }

        if index1 < m && index2 < n && str1_bytes[index1] == str2_bytes[index2] {
            Self::dfs(index1+1, index2+1, current.clone()+&(str1_bytes[index1] as char).to_string(), result, str1_bytes, str2_bytes);
        }

        if index1 < m {
            Self::dfs(index1+1, index2, current.clone()+&(str1_bytes[index1] as char).to_string(), result, str1_bytes, str2_bytes);
        }
        if index2 < n {
            Self::dfs(index1, index2+1, current.clone()+&(str2_bytes[index2] as char).to_string(), result, str1_bytes, str2_bytes);
        }
    }
}
```

Method 2 (AI by Grok3, Dynamic Programming, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$ (M: the length of `str1`, N: the length of `str2`)) :
````rust
impl Solution {
    pub fn shortest_common_supersequence(str1: String, str2: String) -> String {
        // Convert strings to vectors of characters for O(1) indexed access
        let str1_chars: Vec<char> = str1.chars().collect();
        let str2_chars: Vec<char> = str2.chars().collect();
        let m = str1_chars.len();
        let n = str2_chars.len();

        // Initialize DP table with dimensions (m+1) x (n+1)
        // dp[i][j] represents the length of SCS for str1[0..i] and str2[0..j]
        let mut dp = vec![vec![0; n + 1]; m + 1];

        // Fill first row: SCS of empty str1 and str2[0..j] is str2[0..j]
        for j in 0..=n {
            dp[0][j] = j;
        }

        // Fill first column: SCS of str1[0..i] and empty str2 is str1[0..i]
        for i in 1..=m {
            dp[i][0] = i;
        }

        // Fill the DP table
        for i in 1..=m {
            for j in 1..=n {
                if str1_chars[i - 1] == str2_chars[j - 1] {
                    // If characters match, take diagonal value and add 1
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    // If characters differ, take minimum of up or left plus 1
                    dp[i][j] = dp[i - 1][j].min(dp[i][j - 1]) + 1;
                }
            }
        }

        // Reconstruct the SCS by tracing back through the DP table
        let mut result = Vec::new();
        let mut i = m;
        let mut j = n;

        while i > 0 || j > 0 {
            if i > 0 && j > 0 && str1_chars[i - 1] == str2_chars[j - 1] {
                // Characters match: include once and move diagonally
                result.push(str1_chars[i - 1]);
                i -= 1;
                j -= 1;
            } else if i > 0 && (j == 0 || dp[i - 1][j] < dp[i][j - 1]) {
                // Take from str1 if it's shorter or str2 is exhausted
                result.push(str1_chars[i - 1]);
                i -= 1;
            } else {
                // Take from str2 otherwise
                result.push(str2_chars[j - 1]);
                j -= 1;
            }
        }

        // Since we built the string in reverse, reverse it and collect into String
        result.reverse();
        result.into_iter().collect()
    }
}
````
