![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 506. [Relative Ranks](https://leetcode.com/problems/relative-ranks)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```rust
impl Solution {
    pub fn find_relative_ranks(score: Vec<i32>) -> Vec<String> {
        let SPECIAL_RANK: [String; 3] = ["Gold Medal".to_string(), "Silver Medal".to_string(), "Bronze Medal".to_string()];
        let n: usize = score.len();
        let mut score_sort: Vec<(usize, &i32)> = score.iter().enumerate().collect();
        score_sort.sort_by(|a, b| b.1.cmp(a.1));
        let mut result: Vec<String> = vec!["".to_string(); n];
        for (rank, &(index, _)) in score_sort.iter().enumerate() {
            if rank < 3 {
                result[index] = SPECIAL_RANK[rank].clone();
            } else {
                result[index] = (rank+1).to_string();
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```python
class Solution:
    def findRelativeRanks(self, score: List[int]) -> List[str]:
        n = len(score)
        result: list[str] = [None] * n
        rank = sorted(enumerate(score), key=lambda info: info[1], reverse=True)
        for place, (index, _) in enumerate(rank):
            title: str = str(place+1)
            if place <= 2:
                match place:
                    case 0:
                        title = "Gold Medal"
                    case 1:
                        title = "Silver Medal"
                    case 2:
                        title = "Bronze Medal"

            result[index] = title

        return result
```

Method 2 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```python
BASE_MAP = {
    0: "Gold Medal",
    1: "Silver Medal",
    2: "Bronze Medal"
}
class Solution:
    def findRelativeRanks(self, score: List[int]) -> List[str]:
        n = len(score)
        result: list[str] = [None] * n
        rank = sorted(enumerate(score), key=lambda info: info[1], reverse=True)
        for place, (index, _) in enumerate(rank):
            result[index] = BASE_MAP[place] if place <= 2 else str(place+1)

        return result
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$):
```go
import "fmt"

var BASE_RANK = [3]string{"Gold Medal", "Silver Medal", "Bronze Medal"}
func findRelativeRanks(score []int) []string {
    n := len(score)
    var sort_score = make([][]int, n)
    for index, s := range score {
        /* Option 1 */
        sort_score[index] = append(sort_score[index], []int{index, s}...)
        /* Option 2

        sort_score[index] = append(sort_score[index], index, s)
        */
    }
    slices.SortFunc(sort_score, func (a, b []int) int {
        return cmp.Compare(b[1], a[1])
    })

    var result = make([]string, n)
    for rank, item := range sort_score {
        if rank < 3 {
            result[item[0]] = BASE_RANK[rank]
        } else {
            result[item[0]] = fmt.Sprintf("%d", rank+1)
        }
    }
    return result
}
```
