
# Tabu Search for Scheduling Problem

This Python script implements a **Tabu Search Algorithm** to optimize scheduling for a Directed Acyclic Graph (DAG). The task is to minimize **tardiness** in a job scheduling problem, considering **tolerance** and **tabu list length** as key parameters. The script uses **matplotlib** to visualize the results in 2D and 3D plots.

## Table of Contents

1. **Setup and Requirements**
2. **Algorithm Overview**
3. **Functions**
4. **Running the Script**
5. **Visualizing Results**
6. **Brute Force Optimization**
7. **License**

---

## 1. Setup and Requirements

This script requires the following Python libraries:

- **numpy**: For array manipulation and numerical computations.
- **matplotlib**: For plotting graphs and visualizations.
- **collections**: For deque data structure used in Tabu Search.
  
To install the necessary libraries, you can use:

```bash
pip install numpy matplotlib
```

---

## 2. Algorithm Overview

This script optimizes a scheduling problem defined by:
- A **DAG** that dictates the dependencies between tasks.
- A list of **processing times** `p` and **due dates** `d` for each task.
- A **Tabu Search Algorithm** that iteratively improves an initial solution by exploring neighboring schedules, swapping tasks while avoiding revisiting previously explored solutions (using a **tabu list**).

### Key Parameters:
- **Tolerance**: Controls how much worse a solution can be before it's accepted. It helps in finding a balance between exploration and exploitation in the search.
- **Tabu List Length**: The length of the tabu list, which restricts the search from revisiting recently swapped solutions.

---

## 3. Functions

### `get_all_reachable(dag)`
This function returns all nodes that a given node can reach either directly or transitively using the **Floyd-Warshall algorithm**.

### `generate_initial_solution(dag)`
Generates an initial solution for the scheduling problem by performing a **topological sort** of the DAG.

### `is_valid_swap(job_i, job_j, reachable)`
Checks whether swapping two tasks `job_i` and `job_j` is valid based on the DAG's constraints.

### `generate_neighboring_schedule(schedule, swap_index, reachable)`
Generates a neighboring schedule by swapping tasks `job_i` and `job_j` at the given indices.

### `evaluate_tardiness(schedule, p, d)`
Evaluates the tardiness of a given schedule by calculating the total tardiness across all tasks in the schedule.

### `tabu_search(dag, p, d, num_iterations=100, tolerance=10, tabu_list_length=20, verbose=False)`
Implements the Tabu Search algorithm to optimize the schedule. It iterates through neighboring schedules, avoiding tabu solutions and accepting improvements if they reduce tardiness or are within the tolerance threshold.

---

## 4. Running the Script

The script performs the following steps:
1. **Initial Setup**: Defines the DAG, processing times `p`, and due dates `d`.
2. **Tabu Search Execution**: Runs the Tabu Search algorithm with different configurations of tolerance and tabu list lengths.
3. **Evaluation and Visualization**: Computes tardiness values and generates 2D and 3D plots for better understanding of how tolerance and tabu list length affect the tardiness.

---

## 5. Visualizing Results

### 2D Plots
The script generates two 2D plots to visualize the relationship between **tardiness** and two parameters:
1. **Tardiness vs Tolerance** (for a fixed tabu list length).
2. **Tardiness vs Tabu List Length** (for a fixed tolerance).

### 3D Plot
A 3D surface plot is generated showing **tardiness** as a function of **tolerance** and **tabu list length**. This plot helps visualize how the combination of these parameters impacts the performance of the algorithm.

```python
fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(111, projection='3d')
surf = ax.plot_surface(tol, tabu, tardiness_grid, cmap='viridis', edgecolor='k')
fig.colorbar(surf, ax=ax, shrink=0.5, aspect=10)
```

### Example of 3D plot title:  
"**Total Tardiness as a Function of Tolerance and Tabu List Length**".

---

## 6. Brute Force Optimization

After running the **Tabu Search**, a brute force approach is used to find the **optimal solution** by iterating over all combinations of **tolerance** and **tabu list length**. This provides an exact comparison of the best solution found through Tabu Search versus the theoretical best result.

```python
# brute force finding the optimal solution
tardinesses = []
best_s = []
best_t = 1000
best_l = None
best_tol = None
for L in tabu_list_lengths:
    for tolerance in tolerances:
        schedule, tardiness = tabu_search(dag, p, d, tolerance=tolerance, tabu_list_length=L, num_iterations=20000)
        tardinesses.append((schedule, tardiness, tolerance, L))
        if tardiness < best_t:
            best_t, best_s, best_l, best_tol = tardiness, schedule, L, tolerance
```

---

## 7. License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
