![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2115. [Find All Possible Recipes From Given Supplies](https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N*K)$, Space Complexity: $O(N+P)$ (M: average iterations of outer while loop, N: the number of elements in `recipes`, P: the number of elements in `supplies`, K: average ingredients per recipe)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_all_recipes(recipes: Vec<String>, ingredients: Vec<Vec<String>>, supplies: Vec<String>) -> Vec<String> {
        let n: usize = recipes.len();
        let mut supplies: HashSet<String> = HashSet::from_iter(supplies);
        let mut result: Vec<String> = Vec::new();
        let mut has_new_supply: bool = true;
        while has_new_supply {
            has_new_supply = false;
            for index in 0..n {
                if supplies.contains(&recipes[index]) {
                    continue;
                }

                let mut amount_needed: usize = 0;
                for ingredient in &ingredients[index] {
                    if !supplies.contains(ingredient) {
                        break;
                    }

                    amount_needed += 1;
                }
                if amount_needed == ingredients[index].len() {
                    supplies.insert(recipes[index].clone());
                    has_new_supply = true;
                    result.push(recipes[index].clone());
                }
            }
        }

        return result
    }
}
```
