# Freight Container Optimization Problem

## Problem Statement

A logistics company needs to optimize the use of a freight container for an overseas shipment. The container has a **maximum weight capacity of 10,000 kg**. The company has **500 packages**, each with a specific weight and value, representing their importance to the shipment.

The objective is to select a subset of packages that:
1. **Maximizes the total value** of the shipment.
2. Ensures that the **total weight** of selected packages does not exceed the container's capacity.

This is a classic **Knapsack Problem**, which can be solved using techniques such as dynamic programming or greedy algorithms, depending on the constraints and computational requirements.

---

## Solution Approach

### 1. Understanding the Problem

The problem can be modeled mathematically as follows:
- Let the weight of the \(i^{th}\) package be \(w_i\) and its value \(v_i\).
- Define a binary decision variable \(x_i\):
  - \(x_i = 1\): if package \(i\) is selected.
  - \(x_i = 0\): otherwise.

The optimization problem can then be expressed as:

\[
\text{Maximize: } \sum_{i=1}^{500} v_i \cdot x_i
\]
\[
\text{Subject to: } \sum_{i=1}^{500} w_i \cdot x_i \leq 10,000
\]
\[
x_i \in \{0, 1\}, \forall i = 1, 2, \dots, 500
\]

### 2. Solution Methodology

#### a. Dynamic Programming (Exact Solution)
Dynamic programming can be used to solve the problem exactly, but it may be computationally expensive given the large number of packages.

#### b. Greedy Algorithm (Heuristic)
A heuristic approach involves sorting packages by their value-to-weight ratio (
\( \frac{v_i}{w_i} \)) and selecting packages in descending order until the weight limit is reached.

#### c. Linear Programming Relaxation
For a faster approximate solution, relax the binary constraint on \(x_i\) to allow fractional values. Solve using linear programming and round the results.

### 3. Implementation and Visualization

The implementation consists of:
1. Reading the dataset of packages from the provided file.
2. Computing the optimal subset of packages using one of the above methods.
3. Visualizing the results with:
   - A **comparative table** of selected and unselected packages.
   - A **graph** showing total value vs. weight.

---

## Results and Analysis

![Comparative Table](table.png)

The comparative table provides a detailed breakdown of:
- Packages selected for the shipment.
- Their respective weights and values.

![Graph](graph.png)

The graph illustrates the relationship between total weight and total value, showcasing the efficiency of the selected approach.

---

## Conclusion

The optimization successfully maximized the total value of the shipment within the given weight constraint. This demonstrates the effectiveness of the chosen algorithm for solving large-scale logistical challenges efficiently.

---

**Next Steps**
- Explore hybrid solutions combining dynamic programming and heuristics.
- Implement real-time optimization for dynamic package additions or removals.
