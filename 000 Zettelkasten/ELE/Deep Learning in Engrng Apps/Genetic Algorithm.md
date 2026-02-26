202602261010
Status: #idea
Tags: [[Deep Learning (ELE400)]]

A **Genetic Algorithm (GA)** is a bio-inspired optimization method based on biological evolution through mutations and natural selection. GAs are a subset of **Evolutionary Computation**, the field of bio-inspired optimization.

GAs are suitable for [[Supervised Learning]], [[Unsupervised Learning]], and [[Reinforcement Learning]].

## Representation

In the traditional GA, solutions are encoded as **fixed-length bit strings**. Each position represents a feature, and its value represents how that feature is expressed. The string is evaluated as a collection of structural features with little or no interactions.

## Algorithm

1. **Initialize** a random population of individuals (bit strings).
2. **Repeat** until the new population is complete:
   - **Selection**: Select two parent chromosomes based on [[Fitness Function]] values (higher fitness = higher selection probability).
   - **Crossover**: With a crossover probability, combine parents at a crossover point to form offspring. If no crossover occurs, offspring are exact copies of parents.
   - **Mutation**: With a mutation probability, flip bits at each position in the offspring chromosome.
   - **Accept**: Place new offspring in the new population.
3. **Evaluate** fitness of the new population.
4. **Repeat** from step 2 using the new population.

## Reproduction Operators

- **Crossover**: Two parents are split at a crossover point and recombined to form two offspring.
- **Mutation**: Random bit-flipping in an individual's chromosome.

## Stopping Criteria

- High average or max fitness score in the population.
- Fitness value stops changing (convergence).
- Compute time or cycle limit reached.

## Advantages

- Parallelism: multiple solutions explored simultaneously.
- Wider solution space exploration.
- Handles complex fitness landscapes.
- Resistant to local optima trapping.
- Handles noisy and multi-objective problems.
- No knowledge of the response surface (evaluation function) required.
- Performs well for large-scale optimization.

## Limitations

- Identifying the right fitness function is difficult.
- Defining problem representation is non-trivial.
- Premature convergence can occur.
- Tuning parameters (population size, mutation rate, crossover rate) is challenging.
- Cannot use gradients.
- Not effective for smooth unimodal functions.
- No effective termination criterion.
- Require large number of fitness function evaluations.

## Applications

- Medicine (e.g., breast cancer detection)
- Engineering design (electrical, mechanical, civil, manufacturing, robotics)
- Routing and traveling salesman problem
- Network design and wireless communication
- AI: designing [[Feedforward Neural Network]] architectures (layers, nodes, nonlinearity, learning rate, momentum)
- Data mining and [[Clustering]]
