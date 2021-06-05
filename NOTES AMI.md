# All my AMI notes into 1 page

## lecture 1: Intelligent Agents:

AI - entity that perceives and acts

PEAS

P - performance Measure
E - Environment
A - Actuators
S - Sensors

Describing the problem of the environment:

* Fully Observable/Partially Observable
* Single Agent/Multi Agent
* Deterministic/Sctochastic
* Episodic/Sequential
* Static/Dynamic - if environment can change itself while agent is deliberating
* discrete/continuous - discrete has finite set of possibilities (e.g. chess)

Types of agents:
* Utility based agent
* goal based agent
* model-based agent - takes in how the world evolves to adapt actions of AI
* simple reflex agent

SEARCH



## Exam Preparation notes

Exam 2017:

Question 2: ii

Answer: Recursive Best First Search
        -memory efficient
        -can use heuristic
        -can be used to get out of labyrinth


Question 8:

* a Answer: Vx Vy ( Hero(x) ˄ Name(x,Link) ˄ (x!=y) ) => Save(x,World) ˄ ⌐Save(y,World) THE LAST PART MEANS ONLY

* b Answer: Vx Student(x) ˄ Works(x,Hard) => Pass(x,COMP3006)

Disadvantages of Frame and Effect:

    one axiom per action needed - large branching factor and memory needed


However Successor state axioms are more memory efficient (need to clarify)


Question 10:

ii. a Node 5, 6

Question 9:

i. bagging ensemble learning - 
* advantage is that not likely for many learners to get wrong model
* disadvantage is that computing power

Reinforcement learning
* advantage learning can be done without a complete dataset
        

ii. unstable learning is good for ensemble - we get the average of all unstable learners to get more accurate models



## planning

classical planning - deterministic, observable, static.

Bounded interderminacy (unpredictable effects but possible effects can be listed)

* sensor-less planning - constructs sequential plans that are executed without perdeption. Must achieve goal in all circumstances
e.g. wall of bricks, but you are blind, so you cannot see which bricks are painted. therefore just paint all bricks
* Contingency planning - for partially observable environment and non-deterministic environments, sensing actions and describing different paths for different circumstances
* Execution monitoring and replanning - ignores contingencies during planning, handles them as they arise. Useful when planning time is a concern, as not everything can be planned for
    * constructs a plan involving monitoring whether plan can handle current world conditions
* Continuous planning - plan which is continuously updated. Can handle unexpected circumstances, even if occuring in planning stage
    * can also handle goal change!


HOW TO PLAN:
* Record steps to be performed, and reasons why
* if step fails, use dependency directed *backtracking*

Components of planner:
* Choose which rule to apply next
* Detect when solution found (post-condition, *after each action, check if there*)