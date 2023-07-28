# leet-day14

# Predict the Winner

## Problem Description

You are given an integer array `nums`. Two players are playing a game with this array: player 1 and player 2.

Player 1 and player 2 take turns, with player 1 starting first. Both players start the game with a score of 0. At each turn, the player takes one of the numbers from either end of the array (i.e., `nums[0]` or `nums[nums.length - 1]`) which reduces the size of the array by 1. The player adds the chosen number to their score. The game ends when there are no more elements in the array.

Return `true` if Player 1 can win the game. If the scores of both players are equal, then player 1 is still the winner, and you should also return `true`. You may assume that both players are playing optimally.

## Solution Approach

To determine if Player 1 can win the game, we can use a recursive approach to simulate the game for both players' turns and calculate their scores. We keep track of the current index at both ends of the array and the current turn of the player.

1. We define a recursive function `dfs(i, j, nums, turn)` that takes the current indices `i` and `j`, the array `nums`, and the player's turn (0 for player 1 and 1 for player 2).

2. In the `dfs` function, we check the base cases:
   - If the current indices are out of bounds (`i == nums.size()` or `j == -1`), we return 0.
   - If the current indices cross each other (`i > j`), we return 0.

3. For player 1's turn, we can choose the number from either end of the array and add it to the score. We take the maximum of the scores obtained by choosing the number at index `i` and reducing the array size (`dfs(i + 1, j, nums, 1)`) or choosing the number at index `j` and reducing the array size (`dfs(i, j - 1, nums, 1)`).

4. For player 2's turn, we can choose the number from either end of the array and subtract it from the score. We take the minimum of the scores obtained by choosing the number at index `i` and reducing the array size (`dfs(i + 1, j, nums, 0)`) or choosing the number at index `j` and reducing the array size (`dfs(i, j - 1, nums, 0)`).

5. Finally, in the `PredictTheWinner` function, we call the `dfs` function with the starting indices of the array (`0` and `n - 1`, where `n` is the size of `nums`) and the initial turn as `0` (player 1's turn).

6. If the result of the `dfs` function is greater than or equal to 0, we return `true`, indicating that Player 1 can win the game.

## Complexity Analysis

The time complexity of the solution is O(2^n) since there are 2^n possible subgames to consider in the recursive approach. However, we can optimize the solution using dynamic programming to reduce the time complexity to O(n^2).

The space complexity of the solution is O(n^2) for the memoization table used in the dynamic programming approach.
