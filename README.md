# Knapsack-Problem
# Freight Container Optimization Problem

## Problem Statement

A logistics company is preparing a freight container for overseas shipment. The container has a maximum weight capacity of **10,000 kg**. The goal is to maximize the total value of the shipment by selecting a subset of packages, each with a specific weight and value, without exceeding the container’s weight limit.

The challenge lies in selecting the optimal combination of packages from a total of **500 packages**, where:
- Each package has a **weight** and **value**.
- The solution must not exceed the weight limit of the container.
- The total value of selected packages must be maximized.

This is a classic **Knapsack Problem** in combinatorial optimization.

---

## Solution Approach

The problem is solved using a **Genetic Algorithm (GA)**, a search heuristic inspired by natural evolution. The GA mimics biological evolution processes such as selection, crossover, and mutation to arrive at an optimal solution.

### Steps in the Genetic Algorithm

1. **Initialization**: Generate a random population of potential solutions (binary representations of selected packages).
2. **Fitness Evaluation**: Calculate the fitness of each solution based on the total value and weight. Solutions exceeding the weight limit are considered invalid.
3. **Selection**: Use a tournament-based selection to choose the best individuals for reproduction.
4. **Crossover**: Combine pairs of solutions to create new offspring, inheriting traits from both parents.
5. **Mutation**: Introduce random changes to some solutions to maintain diversity in the population.
6. **Iteration**: Repeat the process for a fixed number of generations or until convergence.

---

## Code Implementation

### Import Libraries and Data
```python
import pandas as pd
import numpy as np
import random
import matplotlib.pyplot as plt

# Load data
data = pd.read_csv("items.csv", sep=";", skiprows=1)
values = data['value'].values
weights = data['weight'].values
```

### Define Parameters
```python
max_weight = 10000
population_size = 200
generations = 1000
crossover_rate = 0.8
mutation_rate = 0.2
```

### Initialize Population
```python
def initialize_population(pop_size, num_items):
    return np.random.randint(2, size=(pop_size, num_items))
```

### Fitness Function
```python
def fitness(individual):
    total_weight = np.sum(individual * weights)
    total_value = np.sum(individual * values)
    if total_weight > max_weight:
        return 0
    return total_value
```

### Selection by Tournament
```python
def selection(population, fitness_scores):
    selected = []
    best_index = np.argmax(fitness_scores)
    best_individual = population[best_index]
    for _ in range(len(population)):
        i, j = random.sample(range(len(population)), 2)
        if fitness_scores[i] > fitness_scores[j]:
            selected.append(population[i])
        else:
            selected.append(population[j])
    selected[0] = best_individual  # Retain the best individual
    return np.array(selected)
```

---

## Results

### Fitness Evolution
The fitness score (total value) of the best solution improves over generations, demonstrating the optimization process.

![Fitness Evolution](fitness_evolution.png)

### Final Solution
The algorithm selects a subset of packages that maximize the value while respecting the weight constraint. Below is a visualization of the selected packages:

![Selected Packages](selected_packages.png)

---

## Conclusion

Using the Genetic Algorithm, the logistics company can efficiently determine the optimal set of packages to include in the freight container. This approach provides a near-optimal solution to a complex problem in a reasonable amount of time.

---

## Screenshots

### Initial Population
![Initial Population](initial_population.png)

### Evolution Process
![Evolution Process](evolution_process.png)

### Final Selection
![Final Selection](final_selection.png)

