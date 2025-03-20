![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3108. [Minimum Cost Walk In Weighted Graph](https://leetcode.com/problems/minimum-cost-walk-in-weighted-graph)

### Solution :

Method 1 (AI by Grok3, Union Set, Time Complexity: $O(M+N+Q)$, Space Complexity: $O(N)$ (M: the number of elements in `edges`, N: the value of `n`, Q: the number of elements in `query`)) :
```rust
struct UnionFind {
    parent: Vec<usize>,
    rank: Vec<i32>,
}

impl UnionFind {
    fn new(n: usize) -> Self {
        let mut parent = vec![0; n];
        let mut rank = vec![0; n];
        for i in 0..n {
            parent[i] = i;
        }
        UnionFind { parent, rank }
    }

    fn find(&mut self, x: usize) -> usize {
        if self.parent[x] != x {
            self.parent[x] = self.find(self.parent[x]); // Path compression
        }
        self.parent[x]
    }

    fn union(&mut self, x: usize, y: usize) {
        let px = self.find(x);
        let py = self.find(y);

        if px == py {
            return;
        }

        if self.rank[px] < self.rank[py] {
            self.parent[px] = py;
        } else if self.rank[px] > self.rank[py] {
            self.parent[py] = px;
        } else {
            self.parent[py] = px;
            self.rank[px] += 1;
        }
    }
}

impl Solution {
    pub fn minimum_cost(n: i32, edges: Vec<Vec<i32>>, query: Vec<Vec<i32>>) -> Vec<i32> {
        let n = n as usize;
        let mut uf = UnionFind::new(n);
        let mut component_and = vec![-1; n]; // -1 means all bits set

        // Step 1: Build connected components
        for edge in &edges {
            let u = edge[0] as usize; // Already 0-based
            let v = edge[1] as usize;
            uf.union(u, v);
        }

        // Step 2: Compute AND for each component
        for edge in &edges {
            let u = edge[0] as usize;
            let v = edge[1] as usize;
            let w = edge[2];
            let root = uf.find(u);
            component_and[root] &= w;
        }

        // Step 3: Answer queries
        query.into_iter().map(|q| {
            let u = q[0] as usize; // Already 0-based
            let v = q[1] as usize;
            let root_u = uf.find(u);
            let root_v = uf.find(v);
            if root_u == root_v {
                component_and[root_u]
            } else {
                -1
            }
        }).collect()
    }
}
````
