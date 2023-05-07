## [Number Of Adjacent Elements With The Same Color](https://leetcode.com/problems/number-of-adjacent-elements-with-the-same-color)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn color_the_array(n: i32, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let mut graph = vec![0; n as usize];
        let mut result = vec![];

        for query in queries.iter() {
            graph[query[0] as usize] = query[1];

            let mut temp = 0;
            for index_graph in 0..graph.len()-1 {
                if graph[index_graph] > 0 && graph[index_graph] == graph[index_graph+1] {
                    temp += 1;
                }
            }
            result.push(temp);
        }

        result
    }
}
```

Method 2 (valid those points before and after colored index) :
```rust
impl Solution {
    pub fn color_the_array(n: i32, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let mut graph = vec![0; n as usize];
        let mut result = vec![];
        let mut temp = 0;

        for query in queries.iter() {
            let index = query[0] as usize;
            let color = query[1];

            for index_graph in [index-1, index+1] {
                // valid index between 0 ~ n-1
                if index_graph < 0 || index_graph >= graph.len() {
                    continue;
                }

                // original color isn't 0 && new color != old color
                if graph[index] != 0 && color != graph[index] {
                    // before colored: 2 neighbor colors both equal
                    if graph[index_graph] == graph[index] {
                        temp -= 1;
                    }
                    // after colored: 2 neighbor colors both equal
                    else if graph[index_graph] == color {
                        temp += 1;
                    }
                }
                // original color is 0 && color in both positions are equal after colored
                else if graph[index] == 0 && graph[index_graph] == color {
                    temp += 1;
                }
            }
            result.push(temp);

            graph[index] = color;
        }

        result
    }
}
```
