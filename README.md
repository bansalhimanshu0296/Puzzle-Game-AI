# Puzzle-Game-AI #

This project was done as a part of CSCI-B-551 Elements of Artificial Intelligence Coursework under Prof. Dr. David Crandall.

## Command to run the program ##

python3 solver2021.py [input-board-filename]



## State Space ## 

All boards that can be reached from the initial board using the moves.

##Initial State ## 
Initial board (misplaced board) that is considered as the input for the given program.

## Goal State ## 
Final arranged board which is the expected output for the given program. In this problem, the goal state is always (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25).

## Successor State ## 
We will get 24 successor states which are as follows: 5 right moves, 5 left moves, 5 up moves, 5 down moves, 2 clockwise and 2 counterclockwise.

## Cost Function ## 
Cost for each step in this implementation is 1

## Approach and design decisions: ##

**Abstraction technique used:** A* search

**Assumption:** A solution always exists.

We implemented the heuristic cost in a newly created ‘heuristic(current state)’ function where we calculate the sum of Manhattan distances. Then we alter the ‘is_goal’ function by defining the goal state and comparing it to the current state to check if we have reached the goal state (returns true if it has reached). In ‘successor(state)’ function, we add loops that calculates the board movements leading to the successor states, i.e., movements including right (5 states), left (5 states), up (5 states), down (5 states), outer clockwise (1 state), inner clockwise (1 state), outer counterclockwise (1 state) and inner counterclockwise (1 state). It returns a list of tuples which contains the current move (eg. R3, L2, U4, D1, Ic, Occ, etc), the cost and the board that we get after the current move. In the ‘solve(initial_board)’ function, we have converted the board in tuple format to a nested list. Then we have defined a dictionary that holds the priority as the key and the value is a list of tuples associated with the key that contains the initial board, cost and path. We have defined a visited list that keeps track of all the visited states. We iterate through the fringe and in each iteration we are finding the minimum priority and extracting one of the elements associated with it. We call the other functions to extract the successor states and we are calculating the cost of the successor state and if the cost is already in the fringe, we will directly append the state into the cost otherwise we add it newly. We repeat this until the goal state is reached and the solution path is returned when the goal state has been reached.

**In this problem, what is the branching factor of the search tree?**
The branching factor of the search tree is 24 because we get 24 successor states (5 right, 5 left, 5 up, 5 down, 1 outer clockwise, 1 outer counterclockwise, 1 inner clockwise and 1 inner counterclockwise).

**If the solution can be reached in 7 moves, about how many states would we need to explore we found it if we used BFS?** 
24^7 + 24^6 + 24^5 + 24^4 + 24^3 + 24^2 + 24^1+ 24^0

## Challanges ##

We first used misplaced tiles as the heuristic but it wasn’t admissible and therefore we tried using basic Manhattan and  Euclidean, but all of these were not admissible as well. We then went back to using (misplaced tiles)/5 heuristic, but it wasn’t admissible either. We then implemented some heuristics like Maximum Manhattan distance which even though were admissible but were not fast enough and were caught in timeouts.

