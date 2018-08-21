# CSE 471 Notes: Lecture 2 (Agents and Environments)

## Specifying an AI Prolem
---

    Def: An agent is the entity in which we are writing algorithms for
        e.g. Robot, shopping agent, thermostat, smart home
    *It makes the decisions about what to do*

## Agent Function
---
    Def: Maps percept histories to actions; in other words, takes environment state and outputs what action to do
    
Example: A Vacuum-cleaner world

    Percepts: information returned by the agent's sensors
        - VC world: location, contents (e.g. diry)
    Actions: What the agent can do
        - Let, right, suck, NoOp
    
Agent function for this example:
    
~~~
function REFLECT_VACUUM_AGENT([location_status]) returns an action
    if status == Dirty then return Suck
    else if location == A then return Right
    else if loation == B then return Left
~~~

## Reflex Agents
---
    Follows recipes or pre-coded behavior; e.g. reacts with specific outputs to specific inputs

    - The above example is a reflex agent

### Partial Observability: Reflex Agents with State
    Percepts: What if the sensors do not report current location?

    What would a reflex agent with no memory do?
        If dirty, suck; if clean, left or right?

## Performance Measure
---
    Definition: Measure that analyzes the environment states that are produced by executing an agent function
        - Is used to evaluate the agent function 

    However, sometimes the optimal agent function computation is not computationally possible, so we try to get as close to optimal as possible

## Examples
---

### Example: Shopping Agent
    - Actions (Actuators): Follow URL, fill in form, ask user for information (credit card, address, etc)

    - Sensors: IP packet scanning tools, information retrieval algorithms run on news, product webpages

    - Environment (everything relevant to agent's decision-making): WWW site, vendors/repositories, user activity

    - Performance measure: Price, appropriateness (match to user's preferences), time to place the order, quality of the item

### Example: Household Robot
    - Actuators: Move the joint, cameras, microphones
    
    - Sensors: Touch sensors, RGBD cameras, LIDAR, mic; objeect deetection algorithms, localizations, etc.

    - Environment: Location of humans, locations of all objects in the household, lighting condition

    - Performance measure: Number of questions asked, time taken to serve, cost of resources used

## Specifying Environments
---
    - A property satisfies the Markov assumptttion iff its value is independent of the past given the present
        e.g. Markovian action model: next state depends only on the current state

    - Environment models are designed to make actions Markovian
    - Markovian assumption applies on the model itself

    - An environment where the environment or utility function is not Markovian

## Types of Environments
---

- Observable: Agent knows the state of environment at all times
    - Yes: Solitaire, Chess
    - Partial: Internet shopping, household robot ( some information is not visible to the robot)

- Deterministic: Effects of actions are expressible as functions: S x A -> S
    - Yes: Solitaire, Chess (some uncertainty with other player)
    - No: Internet shopping, Household Robot ( no certain choice and exact information; uncertainty of what the next state might be )

- Static: Environment does not change if agent does not act
    - Yes: Solitaire
    - No: Chess ( the opponent's move adapts to the environment and acts independently ), Internet shopping ( Items get purchased, etc regardless of robot ), household robot

- Discrete: Environment modeled using discrete variables; discrete timestamps
    - Yes: Solitaire, Chess (Moves are a finite amount of time), Internet shopping (purchases are done at discrete timestamps)
    - No: Household robot ( the actions and decisions are done at a continuous interval)

- Single agent: Problem includes a single decision maker
    - Yes: Solitaire (one player game), Internet shopping (other shoppers effect decision, but are independent in the decision making), Household robot
    - No: Chess (two player game)
    ** There may be other agents effecting the environment, but can be argued that it reduces to a single agents

## Key principles
---
    - Agents use their actuators and sensors to interact with environment
    - Agent unction captures agent's behavior
    - A performance measure is used to evaluate the efficacy of the agent function
    - A perfectly rational agent maximizes performance measure

## Example: Route Planning Agent
---

    State: Current city of the robot
    Action: Move along an edge

Methods of evaluating search algorithms for this problem:
1. Completeness - the algorithm will find a solution if there exists one
2. Soundness - if the algorithm returns a solution, it will be a valid path on the graph
    * Note that if an algorithm returns an incorrect answer, it is complete, but not sound
3. Space complexity - how much memory the algorithm uses to compute
4. Time complexity - time in relation to data it takes the algorithm to complete
5. Optimality - algorithm returns solutions of minimal cost

## Example: PacMan as an Agent
---
    Problem Definition:

    - Action: Move Up/Down/East/West
    - Environment (state variables): Coordinates on the grid, presence of dots
    - Percepts: Full state
    - Performance measure: Number of dots remaining * (-1)

    ** Can convert this problem into a route-planning problem

## State-Space Graph
---
    - Nodes represent distinct states of the environment; edges represent action results
    - Possible in deterministic problems; since the states are very well defined

    Search problem: compute behavior that takes the agent from an initial state to the goal state
        - NOTE: in most problems the graph is too large to specify explicitly

    Implicit representation: specify a generative model
        - Analytical transition function: given s, a, T(s,a) returns a unique next state or a distribution
        - Sample based transition function: given s, a, T(s,a) samples a state according to the distribution T(s,a)

    - Define the search problem with initial state, goal state, transition function, accepting state

## Generalizations of the Search Problem
---

### Deterministic, fully observable problem
    T: S x A -> S; agent observes full state

    "Classical planning": solution is a plan, or a sequence of actions
    e.g. A robot knows the exact sequence of actions to take at a starting state to reach the terminating state

### Deterministic , non-observable
    "Conformant planning": Solution is a plan, but often no solutions exist

