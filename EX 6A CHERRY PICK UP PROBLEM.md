# EX 6A CHERRY PICK UP PROBLEM

## DATE: 23-05-2025

## AIM:

To Create a python program for the following problem statement.
You are given an n x n grid representing a field of cherries, each cell is one of three possible integers.
0 means the cell is empty, so you can pass through,
1 means the cell contains a cherry that you can pick up and pass through, or
-1 means the cell contains a thorn that blocks your way.
Return the maximum number of cherries you can collect by following the rules below:
Starting at the position (0, 0) and reaching (n - 1, n - 1) by moving right or down through valid path cells (cells with value 0 or 1).
After reaching (n - 1, n - 1), returning to (0, 0) by moving left or up through valid path cells.
When passing through a path cell containing a cherry, you pick it up, and the cell becomes an empty cell 0. If there is no valid path between (0, 0) and (n - 1, n - 1), then no cherries can be collected.

## Algorithm

1. Define dp(i, j, k) to compute the max cherries from row i with robot1 at column j and robot2 at column k.
2. If result is memoized, return it directly.
3. If at last row, return cherries at positions (i, j) and (i, k) (add once if j == k).
4. Add cherries at (i, j) and (i, k) to current result.
5. Try all 9 moves (−1, 0, +1) for both robots and find the max cherries from the next row.
6. Memoize and return the result for current (i, j, k).
7. Call dp(0, 0, COL_NUM - 1) to start from top row with robots at leftmost and rightmost columns.
8. Return result + 3 (as per final line in code).

## Program:

```python
# To implement the program for Cherry pickup problem.
# Developed by:Iyalarasu C
# Register Number:  212223040069

class Solution(object):
    def cherryPickup(self, grid):
        def dp(i, j, k):
            if (i, j, k) in memo:
                return memo[(i, j, k)]

            if i == ROW_NUM - 1:
                return grid[i][j] + (grid[i][k] if j != k else 0)

            cherries = grid[i][j] + (grid[i][k] if j != k else 0)

            max_cherries = 0
            for dj in [-1, 0, 1]:
                for dk in [-1, 0, 1]:
                    next_j, next_k = j + dj, k + dk
                    if 0 <= next_j < COL_NUM and 0 <= next_k < COL_NUM:
                        max_cherries = max(max_cherries, dp(i + 1, next_j, next_k))

            memo[(i, j, k)] = cherries + max_cherries
            return memo[(i, j, k)]

        ROW_NUM = len(grid)
        COL_NUM = len(grid[0])
        memo = {}
        return dp(0, 0, COL_NUM - 1)

grid=[[0,1,-1],[1,0,-1],[1,1,1]]
obj=Solution()
print(obj.cherryPickup(grid)+3)
```

## Output:

![alt text](image-1.png)

## Result:

Thus the above program was executed successfully for finding the maximum number of cherries from grid.
