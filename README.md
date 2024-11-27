## Scheduling and Resource Allocation Coursework

## scheduling_LCL.ipynb

This Jupyter notebook implements a **Least Cost Last Rule** to optimize scheduling for a given workflow, with an objective of minimizing the maximum cost.

## 1. Setup and Requirements

This script requires the following Python libraries:

- **numpy**: For array manipulation and numerical computations.

## 2. Functions

### `build_graph(edges)`
This function returns an inverted graph mapping successors to predecessors through an adjacency list and a dictionary mapping each node to its number of succesors, given the dag.

### `tardiness(C, dd)`
Calculates the tardiness given a completion time and due date for a job

### `least_cost_last(dag, processing_times, due_dates)`

Implements the Least Cost Last Rule to optimize the schedule by minimizing the maximum cost. The algorithm iterates backwards, determining all available jobs to be scheduled last by checking which have no successors left to be scheduled. Then, it computes the cost for each job to be scheduled last and schedules the one with least cost. We then reduce the number of successors for jobs that preceeded the currently scheduled job and continue the process.

---

## 3. Running the Script

The last cell will execute the LCL rule, taking in the dag, processing times, and due dates defined in the first cell of the notebook. It will then print various iterations of the algorithm with the corresponding schedule at that time and the final iteration with the final cost of the schedule.

---

## coursework.ipynb
This Jupyter notebook implements a **Tabu Search Algorithm** to optimize scheduling for a given workflow, with an objective of minimizing tardiness.

## 1. Setup and Requirements

This script requires the following Python libraries:

- **numpy**: For array manipulation and numerical computations.
- **matplotlib**: For plotting graphs and visualizations.

## 2. Functions

### `get_all_reachable(dag)`
This function returns all nodes that a given node can reach either directly or transitively (only direct connections required for this coursework, as we are only considering adjacent swaps).

### `generate_initial_solution(dag)`
Generates an initial solution for the scheduling problem by performing a **topological sort** of the dag.

### `is_valid_swap(job_i, job_j, reachable)`
Checks whether swapping two tasks `job_i` and `job_j` is valid based on the DAG's constraints.

### `generate_neighboring_schedule(schedule, swap_index, reachable)`
Generates a neighboring schedule by swapping tasks `job_i` and `job_j` at the given indices.

### `evaluate_tardiness(schedule, p, d)`
Evaluates the tardiness of a given schedule by calculating the total tardiness across all tasks in the schedule.

### `tabu_search(dag, p, d, num_iterations=100, tolerance=10, tabu_list_length=20, verbose=False)`
Implements the Tabu Search algorithm to optimize the schedule. It iterates through neighboring schedules, avoiding tabu solutions and accepting improvements if they reduce tardiness or are within the tolerance threshold of an intermediate / current solution. In order to see the status of the Tabu Search (current schedule, current tardiness, neighboring schedule, neighboring tardiness, best schedule, best tardiness, etc.), you should run tabu_search with verbose = True. An example printout of our Tabu Search implementation is found in prinout.txt.

---

## 3. Running the Script

The script performs the following steps:
1. **Initial Setup**: Defines the dag, processing times `p`, and due dates `d`.
2. **Tabu Search Execution**: Runs the Tabu Search algorithm with different configurations of tolerance and tabu list lengths.
3. **Evaluation and Visualization**: Computes tardiness values and generates 2D and 3D plots for better understanding of how tolerance and tabu list length affect the tardiness.

---

## 4. Visualizing Results

### 2D Plots
The script generates two 2D plots to visualize the relationship between **tardiness** and two parameters:
1. **Tardiness vs Tolerance** (for a fixed tabu list length).
2. **Tardiness vs Tabu List Length** (for a fixed tolerance).

### 3D Plot
A 3D surface plot is generated showing **tardiness** as a function of **tolerance** and **tabu list length**. This plot helps visualize how the combination of these parameters impacts the performance of the algorithm.

---

## 5. Brute Force Optimization

After running the **Tabu Search**, a brute force approach is used to find the **optimal solution** by iterating over all combinations of **tolerance** and **tabu list length**.

