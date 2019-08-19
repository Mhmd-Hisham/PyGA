# OptivolutionPy
A flexible genetic algorithm library written purly in Python3.

## Installation

For python3, simply run:
```sh
$ pip3 install OptivolutionPy

```

Or clone this repository and run python3 setup.py install from within the project directory. e.g.:
```sh
$ git clone https://github.com/Mhmd-Hisham/OptivolutionPy.git
$ cd OptivolutionPy
$ python3 setup.py install
```

## Advanced Example
#### Smart Ants using OptivolutionPy & Processing3. check this [repo](https://github.com/Mhmd-Hisham/SmartAntsGA) for more details.

![SmartAntsExample](https://raw.githubusercontent.com/Mhmd-Hisham/SmartAntsGA/master/SmartAnts.gif)
![Test1Example](https://raw.githubusercontent.com/Mhmd-Hisham/test/master/poetry.gif)
![Test2Example](https://warehouse-camo.cmh1.psfhosted.org/1da65858f6b005e253d80acae773d0b0d6b75a74/68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f7364697370617465722f706f657472792f6d61737465722f6173736574732f696e7374616c6c2e676966)
![test3Example](https://raw.githubusercontent.com/Mhmd-Hisham/test/master/SmartAnts.gif)



## Simple example
### Solving the one-dimensional [knapsack problem](http://en.wikipedia.org/wiki/Knapsack_problem):

```python3
#!/usr/bin/env python3

import random

from optivolution.population import Population
from optivolution.chromosome import Chromosome

class OneDimensinalKnapsack(Chromosome):
    """ Inidividual knapsack object. """
    maximum_weight = 15
    knapsack_data = [{'name': 'box1', 'value': 4, 'weight': 12},
                     {'name': 'box2', 'value': 2, 'weight': 1},
                     {'name': 'box3', 'value': 10, 'weight': 4},
                     {'name': 'box4', 'value': 1, 'weight': 1},
                     {'name': 'box5', 'value': 2, 'weight': 2}]
    
    def __init__(self, genes_length=len(knapsack_data), genes=[]):
        super().__init__(genes_length, genes)
    
    @Chromosome.fitness_property
    def fitness(self):        
        """ Defining the fitness function. """
        # Use the knapsack value as the fitness value
        total_value = 0
        total_weight = 0
        
        for i in range(self.genes_length):
            if (self.genes[i] == True):
                total_value += self.knapsack_data[i]['value']
                total_weight += self.knapsack_data[i]['weight']
        
        if total_weight > self.maximum_weight:
            total_value = 0
        
        return total_value
    
    def random_gene(self):
        """ Defining the random gene. """
        return random.choice((0, 1))

class KnapscakPopulation(Population):
    tournament_sample_percentage = 10

    def random_individual(self):
        """ Defining the random individual in the population. """
        return OneDimensinalKnapsack()

def main():
    population = KnapscakPopulation(population_size=20)    
    population.run(20)
    
    print(f"Generation {population.generation_number}")
    best = population.get_best_individual()

    # The optimal answer for this test case is
    # (15, [0, 1, 1, 1, 1])
    print((best.fitness, best.genes))

if __name__ == "__main__":
    main()
```

Output:
```
(15, [0, 1, 1, 1, 1])
```

## Meta

Mohamed Hisham – [G-Mail](mailto:Mohamed00Hisham@Gmail.com) | [GitHub](https://github.com/Mhmd-Hisham) | [LinkedIn](https://www.linkedin.com/in/Mhmd-Hisham/)


This project is licensed under the GNU GPLv3 License - check [LICENSE](https://github.com/Mhmd-Hisham/OptivolutionPy/blob/master/LICENSE) for more details.
