# STA410xiaoCourseProject
Repository for my course project for STA410

STA410xiaoProject.ipynb is a Python package for a maze solver implementing Bayesian deep learning.
All constants can be tweaked at the top of the file.

We started with a simple open room as a maze (no walls) as a sanity check to ensure the deep learning model was functioning.
The simple open room converges quite quickly, as expected, but the algorithm continues to explore for more generations just to make sure.
We added early stopping, if there is no improvement over recent generations/iterations, training is halted.

The agent's step-selection mechanism is exploratory. 
At each step, the agent estimates the distribution of Q-values for each possible action.
It considers both the expected Q-value (mean) and the uncertainty (variance) associated with each action.
Rather than always choosing the action with the highest expected Q-value, the agent will sometimes go for lower Q value actions with high uncertainty.
This allows the agent to explore uncertain areas of the maze, potentially discovering better paths than a purely greedy policy.


For visualization 2 plots are created.
The first shows the layout of the maze, where the agent starts, and the goal.
The second has two subplots and is animated. It can be looped through to show improvements with each generation of the model.
The left subplot is an uncertainty heatmap of the Q values across the maze.
The right subplot traces the agent's path through the maze as it attempts to solve it.

A step counter is included, showing the number of steps the agent takes to reach the goal at each generation.

The next step was increasing complexity.
A pair of simple walls with gaps were added to the maze. Now the agent could no longer move towards the general direction of the goal for the reward. 
Recursive backtracking was implemented to generate complex mazes that are guaranteed to be solvable (perfect mazes).
Randomness was added to the recursive backtracking algorithm to produce loops and branches, resulting in mazes that forced the agent to make decisions at branch points, and reduce the likelihood of trivial solutions (e.g., following a straight hallway).

The agent incurs small penalties for taking steps and attempting to move into walls, while being rewarded for moving closer to the goal and receiving a big reward for reaching it. This helps it learn avoid unnecessary backtracking.

During training, after each generation (or episode), the code prints updates containing
- Generation number (episode)
- current step counts needed to solve the maze
- current best (minimum) step count
- reward accumulated by the end of that training run, the higher the better
