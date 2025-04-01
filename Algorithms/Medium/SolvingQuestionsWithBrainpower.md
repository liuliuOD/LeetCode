![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2140. [Solving Questions With Brainpower](https://leetcode.com/problems/solving-questions-with-brainpower)

### Solution :

Method 1 (AI by Grok3, DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `questions`)) :
```rust
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let n = questions.len();
        let mut dp = vec![-1; n + 1]; // -1 indicates uncomputed

        fn solve(i: usize, questions: &Vec<Vec<i32>>, dp: &mut Vec<i64>) -> i64 {
            if i >= questions.len() {
                return 0; // Base case: no more questions
            }
            if dp[i] != -1 {
                return dp[i]; // Memoized result
            }

            // Solve current question
            let points = questions[i][0] as i64;
            let skip = questions[i][1] as usize;
            let solve_points = points + solve(i + skip + 1, questions, dp);

            // Skip current question
            let skip_points = solve(i + 1, questions, dp);

            dp[i] = solve_points.max(skip_points);
            return dp[i]
        }

        return solve(0, &questions, &mut dp)
    }
}
```
