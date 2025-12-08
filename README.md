# Genetic Scheduling

This project implements a Genetic Algorithm (GA) to solve the exam scheduling problem. It constructs a timetable that minimizes conflicts for students, ensuring that no student has two exams at the same time (hard constraint) and optimizing for other criteria.

## Dataset

I'm using Toronto University dataset, mainly experimenting with uta92 file. So, all data is real, not synthetic

## Installation

To run this project, you need Python installed along with the following dependencies. You can install them using pip:

```bash
pip install matplotlib numpy
```

## Usage

The project is implemented in a Jupyter Notebook: `Arsenii_Palamarchuk_genetic_scheduling.ipynb`.

1.  Open the notebook in Jupyter Lab, Jupyter Notebook, or VS Code.
2.  **Run the code cell by cell** (sequentially) to load the datasets, define the helper functions, and initialize the algorithm.
3.  The final cells contain experiments and visualization of the results.

## Main Algorithm

The core of the project is the `genetic_algorithm` function. It manages the evolution of the population to find the best schedule.

### Parameters

- `pop_size` (int): The number of individuals in the population (default: 50).
- `max_generations` (int): The maximum number of generations to run the algorithm (default: 200).
- `crossover_prob` (float): The probability of performing crossover between two parents (default: 0.8).
- `mutation_prob` (float): The probability of mutating an individual (default: 0.1).
- `tournament_k` (int): The size of the tournament for selection (default: 30).
- `max_time_slots` (int): The total number of available time slots for exams (default: 50).
- `verbose` (bool): If `True`, prints the progress and best fitness at every 10th generation.
- `n_jobs` (int): The number of parallel processes to use for fitness calculation. Set to `None` to use all available cores.

## Results and Conclusions

### Comparison with Published Results

By prioritizing hard constraints and adjusting the soft constraints formula, I was able to achieve significantly fewer direct exam conflicts compared to the baseline. This demonstrates the flexibility of the Genetic Algorithm—it can be efficiently adapted to changing requirements. Moreover, even when I enabled soft constraints, the result was still better than the published solution. This was an unexpected but positive outcome.

### Influence of Parameters

#### Mutations
Initial results were poor due to a high mutation probability. With a genome length of several hundred, even a probability of 0.01 leads to a large number of disruptive mutations. I reduced this value to 0.001 to improve stability.

#### Crossover
Conversely, a high crossover probability accelerated convergence. I believe this is because my genome representation (a sequence of time slots) is well-suited for crossover, as it ensures the offspring always remains valid.

#### Number of Generations
Increasing the number of generations consistently improved the results. This suggests that the problem landscape allows for incremental improvement—small changes to a good solution often lead to an even better one.

### Multithreading
As discussed in the lecture, genetic computations are highly parallelizable. When the soft fitness calculation became a bottleneck, I implemented parallel processing to speed up the execution.

### Conclusion
This problem is a perfect fit for a Genetic Algorithm. Changes in requirements (and the fitness function) lead to corresponding changes in the result, which is exactly the desired behavior.
