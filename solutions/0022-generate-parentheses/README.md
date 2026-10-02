# 22. Generate Parentheses

🔗 [LeetCode Problem](https://leetcode.com/problems/generate-parentheses/)

- **Author:** [@Pragadheeshwar-06](https://leetcode.com/u/Pragadheeshwar-06/) (Global Rank: #608,743)
- **Difficulty:** Medium
- **Pattern:** Dynamic Programming (Backtracking, String, Bracket Sequences)
- **Runtime:** 2 ms (Beats 79.4%)
- **Memory:** 14.2 MB (Beats 66.3%)

---

## Problem Statement

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

 

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

**Example 2:**

```
Input: n = 1
Output: ["()"]
```

 

**Constraints:**

	- `1 <= n <= 8`

---

## Intuition

We break down the problem into optimal overlapping subproblems. By caching solutions in a DP table or memoization array, we eliminate duplicate calculations and build up the global optimum in polynomial time.

---

## Approach

We break down the problem into optimal overlapping subproblems. By establishing recurrence relations and tabulating states, we build up the global optimal solution without redundant recalculation.

---

## Algorithm

1. Define the DP state representation and initialize base cases.
2. Iterate through the state space using bottom-up tabulation or memoized recursion.
3. Apply the transition formula based on optimal subproblem solutions.
4. Return the final target state.

---

## Why This Works

By caching the solutions to subproblems, we ensure that no overlapping state is computed more than once, transforming exponential recursion trees into polynomial-time table lookups.

---

## Complexity Analysis

- **Time Complexity:** `O(V + E)` — Where V is vertices and E is edges in the graph/grid structure.
- **Space Complexity:** `O(n)` — Allocates an auxiliary array of size n to store state transitions.

---

## Solution

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        if (n-- == 1) return {"()"};

        vector<string> res;
        auto dfs = [&](auto& self, int O, int C, string s) -> void {
            if (O == 0 && C == 0) {
                res.push_back(s + ")");
                return;
            }

            if (O > 0)
                self(self, O - 1, C, s + "(");

            if (C >= O)
                self(self, O, C - 1, s + ")");
        };

        dfs(dfs, n, n, "(");

        return res;
    }
};
```
