![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 310. [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees)

### Solution :

Method 1 (Topological Sort variant, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```rust
use std::collections::VecDeque;
impl Solution {
    pub fn find_min_height_trees(n: i32, edges: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = n as usize;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        let mut ingress: Vec<i32> = vec![0; n];
        for edge in edges.into_iter() {
            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            graph[a].push(b);
            graph[b].push(a);

            ingress[a] += 1;
            ingress[b] += 1;
        }

        let mut queue: VecDeque<usize> = VecDeque::new();
        for (index, &amount) in ingress.iter().enumerate() {
            if amount == 0 || amount == 1 {
                queue.push_back(index);
            }
        }

        let mut result: Vec<i32> = vec![];
        while queue.len() > 0 {
            result = vec![];
            let amount: usize = queue.len();
            for _ in 0..amount {
                let index: usize = queue.pop_front().unwrap();
                result.push(index as i32);
                for &index_next in graph[index].iter() {
                    ingress[index_next] -= 1;
                    if ingress[index_next] == 1 {
                        queue.push_back(index_next);
                    }
                }
            }
        }
        return result
    }
}
```

### Solution :

Method 1 (Topological Sort variant, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if n == 1:
            return [0]

        graph = defaultdict(list)
        ingress = [0] * n
        for start, end in edges:
            graph[start].append(end)
            graph[end].append(start)
            ingress[start] += 1
            ingress[end] += 1

        queue = deque()
        for index in range(n):
            """
            there is exactly 1 edge between 2 nodes, so we can say the node is leaf if ingress[index] is 1

            To prevent duplicate calculations, need to substract 1 from `ingress[index]`
            """
            if ingress[index] == 1:
                queue.append(index)
                ingress[index] -= 1

        result = []
        while queue:
            result = []
            amount = len(queue)
            for _ in range(amount):
                index = queue.popleft()
                result.append(index)
                for index_next in graph[index]:
                    ingress[index_next] -= 1
                    if ingress[index_next] == 1:
                        queue.append(index_next)

        return result
```

Method 2 (Topological Sort variant, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(n)]
        ingress = [0] * n
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)
            ingress[a] += 1
            ingress[b] += 1

        # Option 1
        removal = deque([index for index in range(n) if ingress[index] == 1])
        result = set(range(n))
        while len(result) > 2:
            amount = len(removal)
            for _ in range(amount):
                index = removal.popleft()
                result.remove(index)
                for index_connected in graph[index]:
                    ingress[index_connected] -= 1
                    if ingress[index_connected] == 1:
                        removal.append(index_connected)

        return list(result)
        """
        # Option 2

        result = [index for index in range(n) if ingress[index] in [0, 1]]
        removal = deque(result)
        while removal:
            temp = []
            amount = len(removal)
            for _ in range(amount):
                index = removal.popleft()
                for index_connected in graph[index]:
                    ingress[index_connected] -= 1
                    if ingress[index_connected] == 1:
                        temp.append(index_connected)
                        removal.append(index_connected)

            if len(temp) == 0:
                break
            result = temp

        return result
        """
        """
        # Option 3

        result = [index for index in range(n) if ingress[index] in [0, 1]]
        removal = deque(result)
        while removal:
            result = []
            amount = len(removal)
            for _ in range(amount):
                index = removal.popleft()
                result.append(index)
                for index_connected in graph[index]:
                    ingress[index_connected] -= 1
                    if ingress[index_connected] == 1:
                        removal.append(index_connected)

        return result
        """
```

### Solution :

Method 1 (Topological Sort variant + Built-In Queue, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```go
import "container/list"

func findMinHeightTrees(n int, edges [][]int) []int {
    var graph [][]int = make([][]int, n)
    var ingress []int = make([]int, n)
    for _, edge := range edges {
        graph[edge[0]] = append(graph[edge[0]], edge[1])
        graph[edge[1]] = append(graph[edge[1]], edge[0])

        ingress[edge[0]]++
        ingress[edge[1]]++
    }

    queue := list.New()
    for index, amount := range ingress {
        if amount == 0 || amount == 1 {
            queue.PushBack(index)
        }
    }

    var result []int
    for queue.Len() > 0 {
        result = []int{}
        for amount := queue.Len(); amount > 0; amount-- {
            node := queue.Front()
            queue.Remove(node)
            index := node.Value.(int)
            result = append(result, index)
            for _, index_next := range graph[index] {
                ingress[index_next]--
                if ingress[index_next] == 1 {
                    queue.PushBack(index_next)
                }
            }
        }
    }
    return result
}
```

Method 2 (Topological Sort variant + Built-In Slice, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```go
func findMinHeightTrees(n int, edges [][]int) []int {
    var graph [][]int = make([][]int, n)
    var ingress []int = make([]int, n)
    for _, edge := range edges {
        graph[edge[0]] = append(graph[edge[0]], edge[1])
        graph[edge[1]] = append(graph[edge[1]], edge[0])

        ingress[edge[0]]++
        ingress[edge[1]]++
    }

    queue := []int{}
    for index, amount := range ingress {
        if amount == 0 || amount == 1 {
            queue = append(queue, index)
        }
    }

    var result []int
    for len(queue) > 0 {
        result = []int{}
        for amount := len(queue); amount > 0; amount-- {
            index := queue[0]
            queue = queue[1:]
            result = append(result, index)
            for _, index_next := range graph[index] {
                ingress[index_next]--
                if ingress[index_next] == 1 {
                    queue = append(queue, index_next)
                }
            }
        }
    }
    return result
}
```
