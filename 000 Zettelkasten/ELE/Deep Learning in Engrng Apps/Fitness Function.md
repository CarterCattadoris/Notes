202602261011
Status: #idea
Tags: [[Genetic Algorithm]], [[Deep Learning (ELE400)]]

A **Fitness Function** evaluates each individual in a population and assigns it a **Fitness Value**. This function is specific to the problem being solved.

## Role in Genetic Algorithms

In a [[Genetic Algorithm]], the fitness function determines:
- Which individuals are selected for reproduction (higher fitness = higher probability of selection).
- When the algorithm should stop (fitness convergence or satisfactory fitness achieved).

Selection methods vary based on:
- The number of parents chosen.
- How many offspring to create.
- The size of the next generation.
- Which individuals survive to the next generation.

## Challenges

Identifying an appropriate fitness function is one of the key limitations of GAs. The function must accurately represent the quality of a solution for the problem at hand.
