![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2463. [Minimum Total Distance Traveled](https://leetcode.com/problems/minimum-total-distance-traveled)

### Solution :

Method 1 (Backtracking, ERROR: "Time Limit Exceeded", 5/40, Time Complexity: $O(N^M)$, Space Complexity: $O(M)$ (M: the number of the elements in `robot`, N: the number of the elements in `factory`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn minimum_total_distance(robot: Vec<i32>, mut factory: Vec<Vec<i32>>) -> i64 {
        return Self::backtracking(0, &robot, &mut factory)
    }

    fn backtracking(index: usize, robot: &Vec<i32>, factory: &mut Vec<Vec<i32>>) -> i64 {
        if index >= robot.len() {
            return 0
        }

        let mut result: i64 = i64::MAX;
        for index_factory in 0..factory.len() {
            if factory[index_factory][1] <= 0 {
                continue;
            }

            factory[index_factory][1] -= 1;
            result = i64::min(result, (robot[index] as i64).abs_diff(factory[index_factory][0] as i64) as i64 + Self::backtracking(index+1, robot, factory));
            factory[index_factory][1] += 1;
        }

        return result
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(M*N+M*Log(M)+N*Log(N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `robot`, N: the number of the elements in `factory`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn minimum_total_distance(mut robot: Vec<i32>, mut factory: Vec<Vec<i32>>) -> i64 {
        robot.sort();
        factory.sort();
        let mut factory_mapping: Vec<i32> = Vec::new();
        for item in factory {
            for _ in 0..item[1] {
                factory_mapping.push(item[0]);
            }
        }
        let mut memoization: HashMap<(usize, usize), i64> = HashMap::new();
        return Self::dfs(0, 0, &robot, &factory_mapping, &mut memoization)
    }

    fn dfs(index_robot: usize, index_factory: usize, robot: &Vec<i32>, factory_mapping: &Vec<i32>, memoization: &mut HashMap<(usize, usize), i64>) -> i64 {
        if index_robot >= robot.len() {
            return 0
        }
        if index_factory >= factory_mapping.len() {
            return i64::MAX
        }

        let key: (usize, usize) = (index_robot, index_factory);
        if memoization.contains_key(&key) {
            return memoization[&key]
        }

        let mut result: i64 = Self::dfs(index_robot, index_factory+1, robot, factory_mapping, memoization);

        let choose_current: i64 = Self::dfs(index_robot+1, index_factory+1, robot, factory_mapping, memoization);
        if choose_current < i64::MAX {
            result = i64::min(
                result,
                (robot[index_robot] as i64).abs_diff(factory_mapping[index_factory] as i64) as i64 + choose_current
            );
        }

        memoization.insert(key, result);

        return result
    }
}
```

### Solution :

Method 1 (DFS+Memoization, ERROR: "Time Limit Exceeded", 28/40, Time Complexity: $O(M*N+M*Log(M)+N*Log(N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `robot`, N: the number of the elements in `factory`)) :
```java
class Solution {
    public long minimumTotalDistance(List<Integer> robot, int[][] factory) {
        robot.sort(Comparator.naturalOrder());
        Arrays.sort(factory, (a, b) -> Integer.compare(a[0], b[0]));
        ArrayList<Integer> factory_mapping = new ArrayList<Integer>();
        for (int[] item: factory) {
            for (int _unused=0; _unused<item[1]; _unused++) {
                factory_mapping.add(item[0]);
            }
        }
        Map<String, Long> memoization = new HashMap<String, Long>();
        return this.dfs(0, 0, robot, factory_mapping, memoization);
    }

    private long dfs(int index_robot, int index_factory, List<Integer> robot, List<Integer> factory_mapping, Map<String, Long> memoization) {
        if (index_robot >= robot.size()) {
            return 0;
        }
        if (index_factory >= factory_mapping.size()) {
            return Long.MAX_VALUE;
        }

        String key = String.format("%s-%s", index_robot, index_factory);
        if (memoization.containsKey(key)) {
            return memoization.get(key);
        }

        long result = this.dfs(index_robot, index_factory+1, robot, factory_mapping, memoization);
        long choose_current = this.dfs(index_robot+1, index_factory+1, robot, factory_mapping, memoization);
        if (choose_current < Long.MAX_VALUE) {
            result = Math.min(result, Math.abs(robot.get(index_robot)-factory_mapping.get(index_factory)) + choose_current);
        }

        memoization.put(key, result);
        return result;
    }
}
```

Method 2 (DFS+Memoization, ERROR: "Time Limit Exceeded", 36/40, Time Complexity: $O(M*N+M*Log(M)+N*Log(N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `robot`, N: the number of the elements in `factory`)) :
```java
class Solution {
    public long minimumTotalDistance(List<Integer> robot, int[][] factory) {
        robot.sort(Comparator.naturalOrder());
        Arrays.sort(factory, (a, b) -> Integer.compare(a[0], b[0]));
        ArrayList<Integer> factory_mapping = new ArrayList<Integer>();
        for (int[] item: factory) {
            for (int _unused=0; _unused<item[1]; _unused++) {
                factory_mapping.add(item[0]);
            }
        }
        Map<String, Long> memoization = new HashMap<String, Long>();
        return this.dfs(0, 0, robot, factory_mapping, memoization);
    }

    private long dfs(int index_robot, int index_factory, List<Integer> robot, List<Integer> factory_mapping, Map<String, Long> memoization) {
        if (index_robot >= robot.size()) {
            return 0;
        }
        if (index_factory >= factory_mapping.size()) {
            return Long.MAX_VALUE;
        }

        String key = index_robot + "-" + index_factory;
        if (memoization.containsKey(key)) {
            return memoization.get(key);
        }

        long result = this.dfs(index_robot, index_factory+1, robot, factory_mapping, memoization);
        long choose_current = this.dfs(index_robot+1, index_factory+1, robot, factory_mapping, memoization);
        if (choose_current < Long.MAX_VALUE) {
            result = Math.min(result, Math.abs(robot.get(index_robot)-factory_mapping.get(index_factory)) + choose_current);
        }

        memoization.put(key, result);
        return result;
    }
}
```

Method 3 (DFS+Memoization, ERROR: "Time Limit Exceeded", 39/40, Time Complexity: $O(M*N+M*Log(M)+N*Log(N))$, Space Complexity: $O(M*N)$ (M: the number of the elements in `robot`, N: the number of the elements in `factory`)) :
```java
class Solution {
    public long minimumTotalDistance(List<Integer> robot, int[][] factory) {
        robot.sort(Comparator.naturalOrder());
        Arrays.sort(factory, (a, b) -> Integer.compare(a[0], b[0]));
        ArrayList<Integer> factory_mapping = new ArrayList<>();
        for (int[] item: factory) {
            for (int _unused=0; _unused<item[1]; _unused++) {
                factory_mapping.add(item[0]);
            }
        }
        Map<String, Long> memoization = new HashMap<>();
        return this.dfs(0, 0, robot, factory_mapping, memoization);
    }

    private long dfs(int index_robot, int index_factory, List<Integer> robot, List<Integer> factory_mapping, Map<String, Long> memoization) {
        if (index_robot >= robot.size()) {
            return 0;
        }
        if (index_factory >= factory_mapping.size()) {
            return Long.MAX_VALUE;
        }

        String key = index_robot + "-" + index_factory;
        if (memoization.containsKey(key)) {
            return memoization.get(key);
        }

        long result = this.dfs(index_robot, index_factory+1, robot, factory_mapping, memoization);
        long choose_current = this.dfs(index_robot+1, index_factory+1, robot, factory_mapping, memoization);
        if (choose_current < Long.MAX_VALUE) {
            result = Math.min(result, Math.abs(robot.get(index_robot)-factory_mapping.get(index_factory)) + choose_current);
        }

        memoization.put(key, result);
        return result;
    }
}
```
