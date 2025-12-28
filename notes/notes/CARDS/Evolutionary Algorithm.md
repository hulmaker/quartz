---
tags:
  - ML
---

## simple genetic algorithm
1. initialise population (random / informed pre-processing)
2. repeat following steps:
	1. do selection from population 
	2. do crossover
	3. do mutation
	4. fitness evaluation


## selection
some selection algorithms explained [here](http://www.geatbx.com/docu/algindex-02.html)

### Roulette wheel
Probability of choosing some solution is directly proportional to its fitness value
[university lecture](http://www.edc.ncl.ac.uk/highlight/rhjanuary2007g02.php/)

### Tournament selection
1. init tournament: randomly choose N indiv. from population P
2. choose the best indiv. from pool
3. 2. choose the 2nd best indiv. from pool, ... etc, etc ...

### Rank selection
Special case of the [[Evolutionary Algorithm#Roulette wheel]]
Sort samples by fitness, assign them probabilities proportional to their rank (not fitness directly).

## crossover
Given two well-fit solutions to the given problem, it is possible to get a newsolution by properly mixing the two that is even better than both its parents.
**n point crossover**: choose n crossover points (indexes). Then split both parents at chosen points. Alternately mix their segments to get 2 offsprings. (length invariant)
**Cut and splice**: choose one crossover point for each parent. Mix their segments to get 2 offsprings. (length variant)

## mutation
gene manipulation inside one individual.
replacement, random swap, adjecent swap, end-for-end swap, inversion, deletion

## evaluation function
may be almost anything, but it has to be computationaly efficient!

## premature convergence & stagnation
Premature loss of diversity in the population -> sub-optimal solution.
Stagnation: ineffective search due to a weak selective pressure.
Deal with it with balance between exploration and exploitation

## islands model in evolution
On N isolated islands run N independent evolutionary algs. After some iterations, the migration will start.
**migration**: select some individuals, move them to another island
Introduced **by Cohoon et al. (1987)**
Prevents [[Evolutionary Algorithm#premature convergence & stagnation]]

## Elitism
take 1 or more individuals from population P to population P+1 without crossover, mutation etc -> fitness(P+1) >= fitness(P)
Prevents [[Evolutionary Algorithm#premature convergence & stagnation]]