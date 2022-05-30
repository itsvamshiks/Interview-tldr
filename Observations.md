## Observations

### Possible Test cases

 - Invalid/null values for all inputs
 - Empty values for all inputs (length = 0)
 - Edge case values for all inputs
 - 1 or 2 generic test cases
 - Other cases are specific to the problem

### Dynamic Programming

 - When trying to choose between iterate from start / end, see if any indices you're using in populating the DP array mess up accessing the input array. If so, go for iterating from end, else from start
 - When using DP approach for coming up with number of combinations for lets say a target value, always dp[0] = 1, and maybe iterate over number of coin types and the amount remaining(you get it)
 - In recursion, if you can store the value of any outcome, that is DP


### Matrices or Chessboard Paths

 - If you have like a chess board or a matrix type structure and asked to find like number of ways or weights, use combination of adjacent values. For example d[row][col] = d[row][col-1] + d[row-1][col];


### Backtracking

 - For any question, draw a tree on paper and code it looking at it. 


### Linked Lists

 - For every linked list question, attach a dummy node in front of the head before you start coding. At the end, return dummyNode.next; For some questions like LRU cache, you might have to add dummy node at the end


### Arrays

 - For subsequence problems, explore the idea of iterating from the end too, or for that case any array problem

