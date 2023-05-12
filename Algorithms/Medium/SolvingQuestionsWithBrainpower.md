![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Solving Questions With Brainpower](https://leetcode.com/problems/solving-questions-with-brainpower)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded") :
```rust
use std::cmp::max;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let mut results = vec![0; questions.len()];
        for index in 0..questions.len() {
            results[index] = Self::dfs(index, &questions);
        }

        *results.iter().max().unwrap()
    }

    fn dfs(index: usize, questions: &Vec<Vec<i32>>) -> i64 {
        if index >= questions.len() {
            return 0
        }

        let mut temp = questions[index][0] as i64;
        for index_curr in index+(questions[index][1] as usize)+1..questions.len() {
            temp = max(temp, questions[index][0] as i64 + Self::dfs(index_curr, questions));
        }
        temp
    }
}
```

Method 2 (DFS + memoization, ERROR: "Time Limit Exceeded" in 21 / 54) :
```rust
use std::cmp::max;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let mut results = vec![0; questions.len()];
        for index in 0..questions.len() {
            results[index] = Self::dfs(index, &questions);
        }

        *results.iter().max().unwrap()
    }

    fn dfs(index: usize, questions: &Vec<Vec<i32>>) -> i64 {
        if index >= questions.len() {
            return 0
        }

        let mut temp = questions[index][0] as i64;
        for index_curr in index+(questions[index][1] as usize)+1..questions.len() {
            temp = max(temp, questions[index][0] as i64 + Self::dfs(index_curr, questions));
        }
        temp
    }
}
```

Method 3 (DP + memoization, ERROR: "Time Limit Exceeded" in 49 / 54) :
```rust
use std::cmp::max;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let mut results: Vec<i64> = vec![0; questions.len()];
        for index in (0..questions.len()).rev() {
            results[index] = Self::dynamic_programming(index, &questions, &results);
        }

        *results.iter().max().unwrap()
    }

    fn dynamic_programming(index: usize, questions: &Vec<Vec<i32>>, results: &Vec<i64>) -> i64 {
        if index >= questions.len() {
            return 0
        }

        let mut temp = questions[index][0] as i64;
        if index+(questions[index][1] as usize)+1 < questions.len() {
            temp += results[index+(questions[index][1] as usize)+1..results.len()].iter().max().unwrap();
        }
        temp
    }
}
```

Method 4 (DP + memoization, ERROR: "Time Limit Exceeded" in 52 / 54) :
```rust
use std::cmp::max;
use std::collections::HashMap;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let mut hm = HashMap::new();
        let mut results: Vec<i64> = vec![0; questions.len()];
        for index in (0..questions.len()).rev() {
            results[index] = Self::dynamic_programming(index, &questions, &results, &mut hm);
        }

        *results.iter().max().unwrap()
    }

    fn dynamic_programming(index: usize, questions: &Vec<Vec<i32>>, results: &Vec<i64>, hm: &mut HashMap<usize, i64>) -> i64 {
        let mut temp = questions[index][0] as i64;
        let index_next = index+(questions[index][1] as usize)+1;
        if index_next < questions.len() {
            if let Some(maximum) = hm.get(&index_next) {
                return temp + maximum
            }
            hm.insert(index_next, *results[index_next..results.len()].iter().max().unwrap());
            temp += *hm.get(&index_next).unwrap();
        }
        temp
    }
}
```

Method 5 (DP with Bottom Up) :
```rust
use std::cmp::max;
use std::collections::HashMap;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let mut results: Vec<i64> = vec![0; questions.len()];
        let n = questions.len();
        results[n-1] = questions[n-1][0] as i64;
        for index in (0..n-1).rev() {
            Self::dynamic_programming(index, &questions, &mut results);
        }

        *results.iter().max().unwrap()
    }

    fn dynamic_programming(index: usize, questions: &Vec<Vec<i32>>, results: &mut Vec<i64>) {
        let mut point_current = questions[index][0] as i64;
        let index_next = index+(questions[index][1] as usize)+1;
        if index_next < questions.len() {    
            point_current += results[index_next];
        }
        results[index] = max(point_current, results[index+1]);
    }
}
```

Method 6 (DP with Top Down) :
```rust
use std::cmp::max;
impl Solution {
    pub fn most_points(questions: Vec<Vec<i32>>) -> i64 {
        let n = questions.len();
        let mut results = vec![0; n];
        results[n-1] = questions[n-1][0] as i64;
        Self::dfs(0, &questions, &mut results)
    }

    fn dfs(index: usize, questions: &Vec<Vec<i32>>, results: &mut Vec<i64>) -> i64 {
        if index >= questions.len() {
            return 0
        }

        if results[index] > 0 {
            return results[index]
        }

        let mut temp = questions[index][0] as i64;
        let index_next = index + questions[index][1] as usize + 1;
        if index_next < questions.len() {
          temp += Self::dfs(index_next, questions, results);
        }
        results[index] = max(temp, Self::dfs(index+1, questions, results));
        results[index]
    }
}
```
