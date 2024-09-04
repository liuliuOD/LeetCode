![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 874. [Walking Robot Simulation](https://leetcode.com/problems/walking-robot-simulation)

### Solution :

Method 1 (Simulation, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `obstacles`, N: the number of the elements in `commands`)) :
```rust
use std::collections::{HashMap, HashSet};

impl Solution {
    pub fn robot_sim(commands: Vec<i32>, obstacles: Vec<Vec<i32>>) -> i32 {
        let mut mapping_obstacles: HashMap<i32, HashSet<i32>> = HashMap::new();
        for obstacle in obstacles {
            mapping_obstacles.entry(obstacle[0]).and_modify(|set| {set.insert(obstacle[1]);}).or_insert(HashSet::from([obstacle[1]]));
        }

        let mut result: i32 = 0;
        let mut position: Vec<i32> = Vec::from([0, 0]);
        let mut direction: u8 = 0;
        for command in commands {
            match command {
                -2 => {
                    direction -= 1;
                    if direction >= 4 {
                        direction = 3;
                    }
                },
                -1 => {
                    direction += 1;
                    if direction >= 4 {
                        direction = 0;
                    }
                },
                1..=9 => {
                    for _ in 0..command {
                        match direction {
                            0 => {
                                if mapping_obstacles.contains_key(&position[0]) && mapping_obstacles[&position[0]].contains(&(position[1]+1)) {
                                    break;
                                }

                                position[1] += 1;
                            },
                            1 => {
                                if mapping_obstacles.contains_key(&(position[0]+1)) && mapping_obstacles[&(position[0]+1)].contains(&position[1]) {
                                    break;
                                }

                                position[0] += 1;
                            },
                            2 => {
                                if mapping_obstacles.contains_key(&position[0]) && mapping_obstacles[&position[0]].contains(&(position[1]-1)) {
                                    break;
                                }

                                position[1] -= 1;
                            },
                            3 => {
                                if mapping_obstacles.contains_key(&(position[0]-1)) && mapping_obstacles[&(position[0]-1)].contains(&position[1]) {
                                    break;
                                }

                                position[0] -= 1;
                            },
                            _ => {},
                        }
                    }
                },
                _ => {},
            };

            result = result.max(position[0].pow(2) + position[1].pow(2));
        }

        return result
    }
}
```

Method 2 (Simulation, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `obstacles`, N: the number of the elements in `commands`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn robot_sim(commands: Vec<i32>, obstacles: Vec<Vec<i32>>) -> i32 {
        let mut mapping_obstacles: HashSet<(i32, i32)> = HashSet::new();
        for obstacle in obstacles {
            mapping_obstacles.insert((obstacle[0], obstacle[1]));
        }

        let mut result: i32 = 0;
        let mut position: Vec<i32> = Vec::from([0, 0]);
        let mut direction: u8 = 0;
        for command in commands {
            match command {
                -2 => {
                    direction -= 1;
                    if direction >= 4 {
                        direction = 3;
                    }
                },
                -1 => {
                    direction += 1;
                    if direction >= 4 {
                        direction = 0;
                    }
                },
                1..=9 => {
                    for _ in 0..command {
                        match direction {
                            0 => {
                                if mapping_obstacles.contains(&(position[0], position[1]+1)) {
                                    break;
                                }

                                position[1] += 1;
                            },
                            1 => {
                                if mapping_obstacles.contains(&(position[0]+1, position[1])) {
                                    break;
                                }

                                position[0] += 1;
                            },
                            2 => {
                                if mapping_obstacles.contains(&(position[0], position[1]-1)) {
                                    break;
                                }

                                position[1] -= 1;
                            },
                            3 => {
                                if mapping_obstacles.contains(&(position[0]-1, position[1])) {
                                    break;
                                }

                                position[0] -= 1;
                            },
                            _ => {},
                        }
                    }
                },
                _ => {},
            };

            result = result.max(position[0].pow(2) + position[1].pow(2));
        }

        return result
    }
}
```

Method 3 (Simulation, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `obstacles`, N: the number of the elements in `commands`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn robot_sim(commands: Vec<i32>, obstacles: Vec<Vec<i32>>) -> i32 {
        let mut mapping_obstacles: HashSet<(i32, i32)> = HashSet::new();
        for obstacle in obstacles {
            mapping_obstacles.insert((obstacle[0], obstacle[1]));
        }

        let mut result: i32 = 0;
        let mut position: Vec<i32> = Vec::from([0, 0]);
        let mut direction: u8 = 0;
        for command in commands {
            match command {
                -2 => {
                    direction -= 1;
                    if direction >= 4 {
                        direction = 3;
                    }
                },
                -1 => {
                    direction += 1;
                    if direction >= 4 {
                        direction = 0;
                    }
                },
                1..=9 => {
                    for _ in 0..command {
                        let mut x: i32 = position[0];
                        let mut y: i32 = position[1];
                        match direction {
                            0 => {
                                y += 1;
                            },
                            1 => {
                                x += 1;
                            },
                            2 => {
                                y -= 1;
                            },
                            3 => {
                                x -= 1;
                            },
                            _ => {},
                        }

                        if mapping_obstacles.contains(&(x, y)) {
                            break;
                        }

                        position = Vec::from([x, y]);
                    }
                },
                _ => {},
            };

            result = result.max(position[0].pow(2) + position[1].pow(2));
        }

        return result
    }
}
```
