![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2685. [Count The Number Of Complete Components](https://leetcode.com/problems/count-the-number-of-complete-components)

### Solution :

Method 1 (AI by Grok3, Union Find, Time Complexity: $O(E+V)$, Space Complexity: $O(E+V)$ (E: the amount of edges, V: the amount of vertices)) :
```rust
use std::collections::HashSet;

struct UnionFind {
    parent: Vec<usize>,
    rank: Vec<i32>,
    size: Vec<i32>,
}

impl UnionFind {
    fn new(n: usize) -> Self {
        let mut parent = vec![0; n];
        let mut rank = vec![0; n];
        let mut size = vec![1; n];
        for i in 0..n {
            parent[i] = i;
        }

        return UnionFind { parent, rank, size }
    }

    fn find(&mut self, x: usize) -> usize {
        if self.parent[x] != x {
            self.parent[x] = self.find(self.parent[x]);
        }

        return self.parent[x]
    }

    fn union(&mut self, x: usize, y: usize) -> (usize, usize) {
        let px = self.find(x);
        let py = self.find(y);

        if px == py {
            return (px, py);
        }

        if self.rank[px] < self.rank[py] {
            self.parent[px] = py;
            self.size[py] += self.size[px];
            return (py, px);
        } else if self.rank[px] > self.rank[py] {
            self.parent[py] = px;
            self.size[px] += self.size[py];
            return (px, py);
        }

        self.parent[py] = px;
        self.rank[px] += 1;
        self.size[px] += self.size[py];
        return (px, py);
    }
}

impl Solution {
    pub fn count_complete_components(n: i32, edges: Vec<Vec<i32>>) -> i32 {
        let n = n as usize;
        let mut uf = UnionFind::new(n);
        let mut component_edges: Vec<HashSet<(usize, usize)>> = vec![HashSet::new(); n];

        // Build components and collect edges
        for edge in &edges {
            let u = edge[0] as usize;
            let v = edge[1] as usize;
            let (new_root, old_root) = uf.union(u, v);
            // Insert current edge
            component_edges[new_root].insert((u.min(v), u.max(v)));
            // If merging occurred, transfer edges from old root to new root
            if new_root != old_root {
                let old_edges: Vec<_> = component_edges[old_root].iter().copied().collect();
                component_edges[new_root].extend(old_edges);
                component_edges[old_root].clear();
            }
        }

        // Count complete components
        let mut seen = vec![false; n];
        let mut complete_count = 0;

        for i in 0..n {
            let root = uf.find(i);
            if !seen[root] {
                seen[root] = true;
                let size = uf.size[root];
                let edge_count = component_edges[root].len() as i32;
                if edge_count == size * (size - 1) / 2 {
                    complete_count += 1;
                }
            }
        }

        return complete_count
    }
}
```
