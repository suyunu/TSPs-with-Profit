Viewing the Jupyter Notebooks from nbviewer is encouraged because GitHub is still not fully integrated with the Jupyter Notebook:
http://nbviewer.jupyter.org/github/suyunu/TSPs-with-Profit/blob/master/ts-tspp.ipynb

# Tabu Search on Travelling Salesperson Problems with Profits

In this project, we tried to solve Travelling Salesperson Problems with Profits (TSPs with profits) with Tabu Search (TS). Before I start doing anything on the problem, I made a literature survey. There are lots of papers in the literature about TSPs with profits but those papers are generally tries to solve it with some constraints. So actually I couldn't find a good paper to pointing out our problem which has no constraint. But the following paper has some good ideas about the general structer of the problem even it has a constraint on the tour length:
* Gendreau, Michel, Gilbert Laporte, and Frédéric Semet. "A tabu search heuristic for the undirected selective travelling salesman problem." European Journal of Operational Research 106.2-3 (1998): 539-545.

## Travelling Salesperson Problems with Profits

Traveling Salesperson problems with profits (TSPs with profits) are a generalization of the traveling salesman problem (TSP), where it is not necessary to visit all vertices. A profit is associated with each vertex. The overall goal is the simultaneous optimization of the collected profit and the travel costs.
(http://pubsonline.informs.org/doi/abs/10.1287/trsc.1030.0079?journalCode=trsc)

## Solution Representation

I used a simple permutation representation. The list [1, 2, 3, 4, 5, 1] represents the route of the salesperson. All the routes should start with "1" and end with "1" which is the depot.

## Tabu Search

In this part I will explain the steps of tabu search for the travelling salesperson problems with profits.

### Pseudocode

1. **(Initialization)** Construct an initial tour by means of a construction heuristic. 
2. **(Insertion Partitions)** Determine all insertion partitions according to proximity measure and retain 10 of them. 
Repeat Step **3-8** for *$10000$* iterations:
3. **(Insertion Candidate)** Randomly choose one insertion partition and determine the best insertion candidate from this partition 
4. **(Deletion Chains)** Determine the deletion chains. 
5. **(Deletion Candidate)** Determine the best deletion candidate from deletion chains 
6. **(Insertion or Deletion)** Compare the results of the insertion and deletion then apply the best one. If the best move is deletion then declare all vertices of deletion tabu for $\theta$ iteration
7. **(Tour Improvement)** If the iteration count is multiple of 5, apply 2-opt
8. **(Best Solution Update)** If newly generated solution has a better objective then the incumbent solution then apply 3-opt to the newly generated solution to improve the tour quality and make it the incumbent solution.
9. **(Shuffle to Reset)** If there hasn't been an improvement in $\gamma$ iteration, then assign incumbent solution to the current solution and shuffle the route. Also clear the tabu list.
