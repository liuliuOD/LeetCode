![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 332. [Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary)

### Solution :

Method 1 (DFS + Global Variable + Reverse Array) :
```php
class Solution {

    /**
     * @param String[][] $tickets
     * @return String[]
     */
    function findItinerary($tickets) {
        $this->result = [];
        $mapping = [];

        foreach ($tickets as [$from, $to]) {
            $mapping[$from][] = $to;
        }

        foreach ($mapping as &$targets) {
            rsort($targets);
        }

        $this->dfs('JFK', $mapping);
        return array_reverse($this->result);
    }

    function dfs($current, &$mapping) {
        while (!empty($mapping[$current])) {
            $target = array_pop($mapping[$current]);
            $this->dfs($target, $mapping);
        }

        $this->result[] = $current;
    }
}
```

Method 2 (DFS + Reverse Array) :
```php
class Solution {

    /**
     * @param String[][] $tickets
     * @return String[]
     */
    function findItinerary($tickets) {
        $mapping = [];

        foreach ($tickets as [$from, $to]) {
            $mapping[$from][] = $to;
        }

        foreach ($mapping as &$targets) {
            rsort($targets);
        }

        return array_reverse($this->dfs('JFK', $mapping));
    }

    function dfs($current, &$mapping) {
        $result = [];
        while (!empty($mapping[$current])) {
            $target = array_pop($mapping[$current]);
            $result = array_merge($result, $this->dfs($target, $mapping));
        }

        return array_merge($result, [$current]);
    }
}
```

Method 3 (DFS Recursive) :
```php
class Solution {

    /**
     * @param String[][] $tickets
     * @return String[]
     */
    function findItinerary($tickets) {
        $mapping = [];

        foreach ($tickets as [$from, $to]) {
            $mapping[$from][] = $to;
        }

        foreach ($mapping as &$targets) {
            rsort($targets);
        }

        return $this->dfs('JFK', $mapping);
    }

    function dfs($current, &$mapping) {
        $result = [];
        while (!empty($mapping[$current])) {
            $target = array_pop($mapping[$current]);
            $result = array_merge($this->dfs($target, $mapping), $result);
        }

        return array_merge([$current], $result);
    }
}
```

Method 4 (DFS Iterative) :
```php
class Solution {

    /**
     * @param String[][] $tickets
     * @return String[]
     */
    function findItinerary($tickets) {
        $mapping = [];

        foreach ($tickets as [$from, $to]) {
            $mapping[$from][] = $to;
        }

        foreach ($mapping as &$targets) {
            rsort($targets);
        }

        $result = [];
        $stack = ['JFK'];
        while (count($stack)) {
            while (!empty($mapping[end($stack)])) {
                $stack[] = array_pop($mapping[end($stack)]);
            }
            $result[] = array_pop($stack);
        }

        return array_reverse($result);
    }
}
```
