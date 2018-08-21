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

## Example: Shopping Agent
---
    Actions: Follow URL, fill in form, ask user for information (credit card, address, etc)

    Sensors: IP packet scanning tools, information retrieval algorithms run on news, product webpages

    Environment (everything relevant to agent's decision-making): WWW site, vendors/repositories, user activity

    Performance measure: Price, appropriateness (match to user's preferences), time to place the order, quality of the item