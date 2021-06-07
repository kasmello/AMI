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
    * fixes many of the problems in simple reflex agents
* simple reflex agent - takes in the current world state through sensors and decides action based on condition-action mapping
    * only suitable for fully observable world, as it does not consider percept history
        * e.g. when determining whether the front car is breaking or not is based on a single frame of video
    * however the world has to be simple, as we cannot condition-action map everything
    * infinite loops are unavoidable
        * to solve this, when not know what to do, just act random xD
    * also if you don't have a lot of computing power
  

*RATIONALITY* DEPENDS ON:
* Performance measure
* agent's prior knowledge of env
* actions agent can perform
* agent's percept sequence to date
    

## SEARCH

### Uninformed

* Breadth-first search
    * goal test done when node is generated
    * use when you want to find shortest path from certain source node, and branching factor isnt that big
    * does not visit same state multiple times
    * Uses FIFO Queue
    * stops at goal

* uniform-cost
    * uses priority queue
    * The ONLY optimal uninformed search without other terms
    * bad thing about this is space complexity and time complexity much worse than breadth - only use if you only care abt optimality
    * goal test applied to node when it is selected for expansion rather when generated like BFS
    * Takes a lot of space and time as it can explore large trees through small steps before exploring paths with large, useful steps
    * does *NOT* stop at goal

* depth-first search
    * LIFO queue
    * do NOT use on infinitely deep trees!
    * use when not a lot of space is available
    * stops at goal

* depth-limited search
   * nodes after l depth are treated as if they have no more children
   * prevents infinite loops
   * useful if depth of goal is known, or diameter if state space is known

* Iterative deepening depth first search
   * starts at depth of 1, increases every iteration  
   * gets the completeness of BDS, gets linear space complexity of DFS (bd)
   * does not take the same space as BFS, as it is basically separate depth first searches being run one after another, throwing away the memory after each iteration
   * may seem wasted as states are generated multiple times, but most branches are at bottom level, where they will only be generated once

* Bidirectional search - by default uses breadth first search simultaneously from start and end vertex
    * 2 simult-aneous searches - one forward from initial state and other backwards from goal
    * Space complexity can be reduced by roughly half if one of the 2 searches is done by iterative deepening
    * if want to be optimal, additional search after first solution found is required
    * check for solution is done after each node is generated or selected (done with hash table)
    * Advantages
        * Speed of results
        * reduces time taken
        * saves resources
    * Disadvantages
        * more complex to implement
        * only optimal if node cost is the same
        * Need to be aware of goal state is first, as well as states leading up to it
            * in some instances, cannot work backwards

  


### Informed searches

* Greedy best-first search - expands node closest to goal
    * priority queue
    * complexity of space and time = `b^m`
    * susceptible to loops - not complete

* a star

[RBFS and SMA *](http://mas.cs.umass.edu/classes/cs683/lectures-2010/Lec6_Search5-F2010-4up.pdf)

* RBFS
   * Done in linear space
   * but suffers from node regeneration overhead


* SMA star


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

* one axiom per action needed - large branching factor and memory needed


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
* Choose which rule to apply next - planner might look at several moves in advance
    * Generate set of differences between goal and current, identify rules to reduce differences
* Detect when solution found (post-condition, *after each action, check if there*)
* Detect dead-ends, take action
* Detect "almost correct" solution
* Apply rule to compute new state
* Also needs to find a way to handle rules specity partial problems

Successor-state axiom in 1 axiom specifies changes and non changes for different states

*How to hangle "almost correct solution?*
* Approach 1: use different approach and solve problem separately e.g. random search (?)
* Approach 2: use least commitment - no order fixed until we need to do them 


Components of Successor state axioms:
initial state definition
goal state definition - should be checked after each action
Operator definition - what happens after each action
Basic plan

Interaction between sub-goals - important! one goal might conflict with another

[forward and backward](http://epgp.inflibnet.ac.in/epgpdata/uploads/epgp_content/S000305IT/P001484/M017184/ET/1470220705AIModule16.pdf)

Forward Planning - searchs state-space graph from initial state looking for state that satisfies goal description
* the good thing about forward planning is that we know if we are getting closer to goal through heuristics
* In a game such as chess, there may be multiple final nodes, may not know where we are going to reach

Backwards Planning - begins from goals state, tries to reach initial state 
* visibility of goal helps us choose moves - goal directed reasoning - preferred when branching factor in reverse direction less than forward (block world)
* also, moving from known to unknown is better than unknown than knon

Partial order planners - plan which specifies all actions needed to be taken, only specifies and reorders between actions when necesssary
* used in blocks world, or a shopping list in real life
* Partial order plan has:
    * set of actions/operators
    * partial order for actions, specifies conditions about order of some actions
    * casual links - which actions meet which preconditions of other actions
    * open preconditions - specifies preconditions not fulfilled by any action in partial-order plan
* The less partial order/casual links, the more variety of actions there are

* Threat in partial ordering is orderings that threaten to break connected actions: to resolve:
    * Promotion - orders a step to have to precede another step
    * demotion/de-blobbering - orders a step before to "clobber" another step's preconditions

## LOGIC

The problem between frame and effect axioms is the FRAME problem - challenge of expressing the effects of actions without explicitly stating non-changes
* Representation - avoid frame axioms
* inference - avoid "copy-overs" to keep track of state

This is where we can combine them into successor state axioms!
* each axiom on left is about predicate rather than action
* Disadvantages ???

## Machine Learning

2 categories of learning algorithms *NOTE that both will be impacted by noise*

Conceptual learning - if not clean of noise, generalisations will be off.

* non incremental (one step learning) 
    * labelled data
    * generate classification structure (hierarchal)
    * uses classification structure to determine class of new unlabelled instance
        * advantage - simple, generates good and efficient classification structures
        * disadvantages - limited applications, need all data at the start of training, and hard to update

Non incremental learning is not realistic in real world, data is always added and updated

* incremental 

The general procedure is:
* input some training data
* generate concept representation based on data observed
* uses concept representation to classify new daya
* update concept representation to be consistent with data observed - continuously updated
    * advantages - effective in real world
    * disadvantages - difficult to implement

Problems in incremental learning include:
* bias
    * the way data needs to be arranged has to make it easy for the learner to derive a definition of classes
    * things which introduce bias can be:
        * poor quality of training data
        * model performance mismatch - when training data does not match data it will be tested on
* how to store data/representations
    * full memory - retain all examples observed - *NOT* realistic
    * partial memory - selective of what it is you will store
    * have summary statistics to help with classification more effectively (?)
        * used by lots of learners to make a decision on larger sample
* update rate of data/conditions
    * sometimes it is a bad choice tho, if data is full of noise, continuously updating will introduce variance


