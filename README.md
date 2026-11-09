# **Artificial Bee Colony**

**Derviş Karaboğa**
- a Turkish computer scientist and AI researcher best known for developing the Artificial Bee Colony (ABC) Algorithm in 2005, an optimization technique inspired by the food-foraging behavior of honeybees.

---

## **Artificial Bee Colony**
- It is an optimization technique inspired by the intelligent food- foraging behavior of a real bee swarm. It is a swarm-based meta-heuristic algorithm for optimizing numerical problems.
- One of the most popular and widely used nature-inspired metaheuristic algorithms under the population-based swarm intelligence family. Its search process relies on random values to maintain a balance between two important stages: **exploration** and **exploitation**, allowing the algorithm to discover new solutions while improving existing ones.
	- **Exploration** refers to searching new regions or possibilities to discover potential solutions.
	- **Exploitation** refers to refining and improving existing solutions to find better or more optimal results.

###### **Heuristic**
- A problem-specific rules that quickly find an acceptable solution

###### **Meta-Heuristics**
- A high-level, problem-independent procedure designed to find, generate, or select a lower-level heuristic or optimization algorithm to find a sufficiently good solution to a complex problem.
- Metaheuristic algorithms have two major components: diversification and intensification:
1. **Diversification**
	- Ensures that the solution does not become trapped in local optima while exploring the vast search space.
2. **Intensification**
	- Concentrates on best solution for convergence to optimality.

###### **Numerical Optimization**
- The process of finding the best possible solution to a problem using mathematical calculations and numerical methods.
- In simple terms, it means finding the best value among different possible solutions while following certain conditions or limitations.
- Can be used for solving unimodal and multi-modal numerical optimization problems.

###### **Unimodal and Multi-modal**
- **Unimodal** 
	- an optimization problem that has only one optimum or best solution, with no other local optima.
	- Has one optimum and no other local optima.
- **Multi-Modal** 
	- an optimization problem that has multiple local optima, meaning it contains several peaks or valleys.
	- Has many optima.


## **SWARM INTELLIGENCE**
- Inspired by the collective behavior of social insect colonies and other animal societies on making an attempt to design algorithms or distributed problem-solving devices
- Field of study that models the population of swarms or interacting agents with the capacity to self-organize.
- Examples: Artificial Bee Colony, Bee Colony, Ant Colony, Firefly, Cuckoo Search Algorithm
- 2 Concepts of Swarm Intelligent Behavior:
	1. **Self-Organization** refers to the process in which individual components of a system interact with one another to create organized structures or patterns at a global level without requiring centralized control.
	2. **Division of Labor** refers to the process in which different individuals perform specialized tasks simultaneously, allowing the entire system to work more efficiently.
- In the ABC Algorithm:
	- Self-Organization: Bees coordinate their activities through interactions and shared information about food sources.
	- Division of Labor: Employed, onlooker, and scout bees perform different tasks to find the best food sources (solutions).

###### **Balance of Exploration and Exploitation**
- **Excessive exploration**
	- Too much searching; convergence may be slow because the algorithm does not sufficiently refine good solution.
- **Excessive exploitation**
	- The population may be converge prematurely to a local optimum and stop exploring better regions.
- **Convergence** means the solutions are gradually clustering together toward the area with the best fitness, showing that the algorithm is getting closer to the best solution.

###### **Why is it Random?**
- It appears in three main stages: generating the initial population of random food sources, creating neighboring solutions, and allowing scout bees to generate completely new random solutions when an existing food source is abandoned. It helps prevent all bees from focusing on only one region too early. It also allows the algorithm to explore new areas and escape local optima, increasing the possibility of finding the global optimum.

###### **ADVANTAGES**
- Simple, easy to implement, and quick convergence, robustness, and clear benefits when handling combined optimization problems
- Fewer control parameters
- Good balance of exploration/exploitation for many continuous problems
- Has performed well on benchmark functions and real-world engineering problems

###### **DISADVANTAGES**
- Can converge slowly on some problems
- Premature convergence in the later search period
- Exploitation ability can be weaker than some other algorithms, so accuracy isn’t always perfect.

###### **3 ROLES**
- **Employed Bee**
	- Search Food Source
- **Scout Bee**
	- Abandon Exhausted Source. Search Again
- **Onlooker Bee**
	- Pick the Food Source

###### **3 PHASES**
- Employed Bee Phase
	- Employed bees look for a food source that is better than the one they are currently using.
	- generate a new solution using a partner solution
	- greedy selection: if the new solution is better than the current solution, accept the new solution
	
- Scout Bee Phase
	- select a food source with a probability related to nectar amount by waggle dance
	- generate a new solution using a partner solution
	- greedy selection: if the new solution is better than the current solution, accept the new solution
    
- Onlooker Bee Phase
	- exhausted food source is abandoned
	- discard and generate new solution

###### **Real-world usage**
- **Data Mining & Machine Learning**
	- Improve how computers learn from data.
	- Example: Feature Selection
		- Choose only the most useful data columns so a model becomes more accurate and faster
- **Network & Routing Optimization**
	- Find efficient paths and resource arrangements in networks.
	- Example: Routing
		- Finding the shortest or fastest route for data packets, vehicles, or delivery trucks.


---
###### **Algorithm**
Initialize all parameter
	REPEAT
			Send the employed bees onto the food sources and determine their nectar amounts
			Calculate the probability value of the sources with which they are preferred by the onlooker bees
			Send the onlooker bees onto the food sources and determine their nectar amounts
			Stop the exploitation process of the sources exhausted by the bees
			Send the scouts into the search area for discovering new food sources, randomly
			Memorize the best food source found so far
	UNTIL (requirements are met)

Formula

## Formulas & Variable Notation

- $x$ = Current Solution
- $x_{new}$ = Newly Generated Solution
- $f$ = Objective function value of a solution
- $f_{new}$ = Objective function value of new solution
- $fit$ = Fitness of a solution
- $fit_{new}$ = Fitness of a new solution
- $\varphi$ (phi) = random number
    
## Initialize All Parameters

- ** $x$ = Current Solution:**  
    $$x = LB + (UB - LB) \times \text{rand}(0,1)$$
- **$f$ = Objective function value of a solution:**
        
    - _Note: Our program uses the Sphere Function (_$x^2$_) as a benchmark function, but you can use any discussed or outside benchmark._
        
- **Fitness Evaluation:**  
    $$fit = \begin{cases} \frac{1}{1 + f} & \text{if } f \geq 0 \\ 1 + \vert{}f\vert{} & \text{if } f < 0 \end{cases}$$


## Cycle Begin: Employed Bee Phase (E.B.P.)

**Send the employed bees onto the food sources and determine their nectar amounts.**
### Generation of New Solution

- Number of Employed Bees = Number of food sources
- All solutions generate a new solution.
- A partner is randomly selected to generate a new solution (partner $\neq$ current solution).
- A new solution is generated by modifying a randomly selected variable:  
    $$x_{new} = x^j + \varphi (x^j - x^j_p)$$
    _Where:_
    - $x^j$ = $j$-th variable of current solution
    - $\varphi$ = random number between -1 and 1
    - $x^j_p$ = $j$-th variable of partner solution
        

### Selection of New Solution

- Evaluate the objective function and fitness of the newly generated solution.
    
- Perform greedy selection to update the current solution:  
    
    $$\begin{cases} x = x_{new} \\ f = f_{new} \end{cases} \text{if } fit_{new} > fit$$
- **Trial counter:** tracks the number of failures encountered by each.
    - If the new solution is inferior $\rightarrow$ increase the trial of the current solution by 1.
    - If a better solution is generated $\rightarrow$ reset the trial to zero.
        

## Onlooker Bee Phase

**Calculate the probability value of the sources with which they are preferred:**

- The probability value of each solution to undergo the onlooker phase is determined as:  
    $$prob = 0.9 \times \frac{fit}{\max(fit)} + 0.1$$
- A solution with a higher fitness value will have a higher probability.
- A fitter solution may undergo the onlooker bee phase for more than one iteration.
    
**Send the onlooker bees onto the food sources and determine their nectar amounts:**

- If $r < prob$, generate a new solution (where $r$ = random number).
- If the Onlooker Bee (O.B.) found a food source:
    - Generate new $X$.
    - Perform greedy selection.
    - Update if new $X$ has better fitness and reset trial to 0; else increase trial by 1.
- _Stop the exploitation process of the sources exhausted by the bees._
    

## Scout Bee Phase

**Send the scouts into the search area for discovering new food sources, randomly.**
- Candidates to be discarded = solution with `trial > limit`.
- 1 solution with its trial greater than the limit is replaced with a new random solution.
- The trial counter of the newly included solution is reset to zero.
    
**Steps when the food source (**$k$**) has `trial > limit`:**
1. Identify the food source ($k$) whose `trial > limit`.
2. Replace $x_k$ from $P$ as:  
    $$x_k = LB + (UB - LB) \times r$$
3. Evaluate the objective function and assign fitness.

## **Memorize the best food source found so far** 
## **next**
## **Cycle Stop**


###### **Algorithm Flowchart Cycle**

1. **Initialization of Parameters**
2. **Check Termination Criteria Satisfied?**
    - If **Yes (Y)** $\rightarrow$ Best Solution Found So Far
    - If **No (N)** $\rightarrow$ Proceed to next steps:
        1. Update Employed Bees
        2. Update Onlooker Bees
        3. Update Scout Bees
        4. Memorize the Best Food Source
        5. _Loop back to Termination Criteria check._
            

---
###### **Program**s

Prerequisites:

|                | How to installl                                                              |
| -------------- | ---------------------------------------------------------------------------- |
| **python**     | search python install                                                        |
| **numpy**      | a open-source library of python. type in terminal: `pip install numpy`       |
| **matplotlib** | a open-source library oh python. type in terminal : `pip install matplotlib` |

**mainWith2shows.py**
- Simple Program showing how ABC Algorithm works

**TSPAnimation.py**
- Implimenting ABC Algorithm on Traveling Salesman Problem

