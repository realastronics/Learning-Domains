# Artificial Intelligence

## 1. Foundation 
## 1.1) What is AI
Artificial Intelligence (AI) is the field concerned with **understanding and designing computational systems** (models, algorithms, and representations) that exhibit **intelligent, goal-directed** behavior by **perceiving and representing their environment, reasoning and learning from information, solving problems and making decisions**, and autonomously **selecting actions** to achieve specified goals under constraints and uncertainty.

**Intelligence vs. Cognition**:
- **Cognition** is the set of processes by which a system acquires, represents, processes, and uses information — including perception, memory, learning, reasoning, and decision-making.
- **Intelligence** is the broader capacity to use such processes **effectively and adaptively** to achieve goals, particularly when the environment is uncertain, changing, or only partially specified.
## 1.2 ) AI Problems and Non-AI Problems
A problem is not an AI problem merely because it is difficult or computationally expensive. If a complete procedure for solving it can be specified in advance, it generally falls under conventional programming or automation. AI becomes relevant when the **system must determine appropriate actions** or solutions in situations involving uncertainty, incomplete information, alternatives, adaptation, or changing environments.

- **Non-AI problem**: The solution can be sufficiently specified through fixed rules or an algorithm.
  **Example:** Sorting `[7, 2, 9, 4]`
  The system does not need to decide what to do. The algorithm specifies the procedure.
- **AI problem**: The system must determine **what to do or infer** when the correct behavior cannot be completely specified beforehand.
  **Example:** A robot navigating an unfamiliar building. It must interpret observations of environment, consider possible paths, account for obstacles, and choose actions that move it toward its goal.

The boundary however is not absolute. AI systems still rely heavily on conventional computation.
> **AI becomes necessary when specifying every correct action in advance becomes impractical, impossible, or inadequate.**
## 1.3) Approaches to Artificial Intelligence
There are two basic questions we can ask when defining AI:
- *Should a machine **think** like a human or like an ideal reasoner?*
- *Should a machine **act** like a human or act rationally?*

This gives four classical approaches:
1. **Thinking Humanly:** with goal to build systems that reproduce the way humans actually think. \
2. **Acting Humanly:** with goal to build systems whose behavior is indistinguishable from human behavior. The **Turing Test** is the classic example. A machine is considered intelligent if, through conversation, a human evaluator cannot reliably distinguish it from a human. 
   **Limitation:** *human behavior is not necessarily rational or optimal, so imitating humans is not the same as producing intelligent behavior.*
3. **Thinking Rationally:** with the goal to reason according to formally correct principles of logic. For example, given valid premises, derive valid conclusions. This approach is useful for understanding formal reasoning, but real environments are often uncertain, incomplete, and too complex to represent perfectly in logic.
4. **Acting Rationally:** with the goal being to choose actions that are appropriate for achieving the system's goals, given its available information and constraints.

This leads to the **rational-agent approach** where "an intelligent system should choose the action that is expected to produce the best outcome, given what it knows". This approach only requires its behavior to be appropriate for the task and circumstances.

So the progression is:
> **Human imitation → Formal reasoning → Rational action**

The **rational-agent perspective** provides the foundation for how we will study search, planning, reasoning, learning, and modern AI systems.
## 2. Intelligent Agents & Expert Systems

## 2.1) Agents, Rationality & Task Environments
An **agent** is a system that **perceives its environment through sensors and acts upon it through actuators**. The important idea is not that an agent must be human-like, but that it can **use percepts to select actions** in an environment.

A thermostat, robot, chess program, or autonomous vehicle can be an agent because it receives information, processes it, and produces actions or outputs.

**Percept** is the information an agent receives from its environment at a particular moment. **Percept sequence** is the complete history of percepts received by the agent.
```
Percept → camera image + speed + GPS + radar
Action  → accelerate / brake / steer
```

The **agent function** specifies the mapping from the percept sequence to an action:
*f : percept sequence → action*
The **agent program** is the actual computational implementation of the agent function.

---
**Rational agent** is an agent that chooses the action expected to **maximize its performance measure**, given its percept sequence, available knowledge, available actions, and the uncertainty of the environment.
> **Rationality means choosing the best action justified by the information available, not guaranteeing a successful outcome.**

---
A **task environment** is the environment in which an agent operates and whose state can be affected by its actions. The environment can be described using several important properties such as:
1. **Fully observable vs. partially observable:** whether the agent can perceive all relevant aspects of the current state.
2. **Deterministic vs. stochastic:** whether an action's outcome is completely predictable.
3. **Episodic vs. sequential:** whether each decision is independent or affects future decisions.
4. **Static vs. dynamic:** whether the environment can change while the agent is deciding.
5. **Discrete vs. continuous:** whether states, actions, or time have distinct values or vary continuously.
6. **Single-agent vs. multi-agent:** whether other agents also influence the outcome.
7. **Known vs. unknown:** whether the agent knows the rules governing how the environment works.

These properties matter because the **nature of the environment determines the kind of reasoning, representation, planning, and decision-making the agent requires**.

To specify a task environment, we use **PEAS**:
- **P — Performance measure:** how success is evaluated.
- **E — Environment:** the world in which the agent operates.
- **A — Actuators:** the actions the agent can perform.
- **S — Sensors:** the information the agent can perceive.

**Example: Autonomous taxi**

| Component   | Example                              |
| ----------- | ------------------------------------ |
| Performance | Safety, travel time, comfort, cost   |
| Environment | Roads, traffic, pedestrians, weather |
| Actuators   | Steering, brakes, accelerator        |
| Sensors     | Cameras, GPS, radar, lidar           |
## 2.2) Agent Architectures & Problem Solving
An **agent architecture** describes how an agent converts percepts and internal information into actions. The architectures become progressively more capable by introducing **internal state, goals, preferences, and learning**.

There are many kinds of agents as we have noted below:

**Simple Reflex Agent -** It uses direct condition-action rules based only on the **current percept**, (*Percept → Rule → Action*). It's simple and fast, but ineffective when the current percept alone is insufficient to determine the appropriate action. 
Example:
IF temperature < 20°C → turn heater on

**Model-Based Reflex Agent -** It maintains an **internal state** that represents aspects of the world that may not be directly observable.
```
Percept + Previous State
          ↓
    Update Internal State
          ↓
          Rule
          ↓
        Action
```
The internal state acts as a model of how the world changes. This allows the agent to function in **partially observable environments**.

**Goal-Based Agent**
Chooses actions by considering a desired **goal state**.
```
Current State + Goal
        ↓
   Search / Planning
        ↓
      Action
```
Example:
> Goal: Reach Room B.

The agent considers possible sequences of actions and selects one that achieves the goal.

**Utility-Based Agent**
Goals tell an agent whether an outcome is acceptable, but not necessarily **which acceptable outcome is better**. 

A utility function assigns a measure of desirability to outcomes.
```
Possible outcomes
       ↓
  Utility values
       ↓
Choose action with
highest expected utility
```

For example, two routes may both reach the destination, but one may be faster, safer, or cheaper.
> **Goal:** What outcomes are acceptable?  
> **Utility:** How desirable is each outcome?

Utility becomes especially important when outcomes are uncertain or objectives compete.

**Learning Agent**
A learning agent improves its behavior through **experience** rather than relying entirely on knowledge and rules specified beforehand.

A standard learning-agent architecture contains:
- **Performance element:** selects actions.
- **Learning element:** improves the performance element.
- **Critic:** evaluates the agent's performance.
- **Problem generator:** encourages useful exploration.

```
                   ┌──────────────────┐
Environment → Percepts → Performance Element → Actions
                              ↑
                       Learning Element
                              ↑
                            Critic
                              ↑
                           Feedback

                    Problem Generator
                           ↓
                       Exploration
```

The progression is:
```
Simple Reflex
      ↓
Model-Based
      ↓
Goal-Based
      ↓
Utility-Based
      ↓
Learning
```

These architectures are not mutually exclusive. A modern system can maintain an internal model, pursue goals, optimize utility, and learn from experience at the same time.

A **problem-solving agent** is a goal-based agent that formulates a problem and searches for a sequence of actions that reaches a goal.

This creates the bridge to the next major topic:
> **Agent → Goal → Problem Formulation → Search → Action**
## 2.3) Expert Systems
An **expert system** is an AI system designed to solve problems in a specific domain by **combining explicit domain knowledge with an inference mechanism**.

The central idea is:
> **Separate what the system knows from how it reasons with that knowledge.**

Its basic architecture consists of:
```
User
  ↓
User Interface
  ↓
Inference Engine ↔ Knowledge Base
  ↓
Conclusion / Recommendation
```

**Knowledge Base:** stores domain-specific knowledge, commonly as facts and rules.
```
Fact: Patient has a fever.
Rule: IF fever AND cough → possible infection.
```

**Inference Engine:** applies the rules to known facts to derive conclusions.

**Knowledge Acquisition:** the process of obtaining and encoding knowledge from human experts or other sources.

Expert systems were important because they demonstrated that useful intelligent behavior could be produced by **explicitly representing domain knowledge and reasoning over it**. They were used in areas such as diagnosis, configuration, and troubleshooting.

Their main limitation is their dependence on the **quality, completeness, and maintainability of explicitly encoded knowledge**. They struggle when knowledge is difficult to express as rules, situations are novel or uncertain, or the rule base becomes very large and difficult to maintain.

> **Expert system = explicit domain knowledge + inference mechanism + reasoning over that knowledge.**
## 3. Problem Solving & Search

## 3.1) Problem Formulation

A **problem formulation** is a formal description of a problem that specifies what the agent is trying to achieve and the possible actions it can take to get there.

The purpose is to convert a real-world objective into a representation that a search algorithm can solve.

A well-defined search problem consists of five components:

1. **Initial state** — where the agent starts.
2. **Actions** — the actions available to the agent in a given state.
3. **Transition model** — describes the state that results from taking an action.
4. **Goal test** — determines whether a state satisfies the objective.
5. **Path cost** — assigns a cost to a sequence of actions.

```
Initial State
      ↓
  Actions
      ↓
Transition Model
      ↓
 Successor States
      ↓
   Goal Test
      ↓
  Solution + Cost
```

**Example: Route finding**

Suppose the agent must travel from Delhi to Jaipur.

```
Initial state → Delhi
Actions       → Travel to connected cities
Transition    → Moving to a city produces a new location
Goal test     → Current location = Jaipur
Path cost     → Total distance or travel time
```

The solution is a **sequence of actions** that transforms the initial state into a state satisfying the goal.

### State-Space Representation

The **state space** is the set of possible states reachable by the agent through its actions.

A search algorithm explores this space looking for a path from the initial state to a goal state.

```
          Initial
          State
         /      \
        A        B
       / \        \
      C   D        E
          |
        Goal
```

An important distinction:

> **State space = the possible configurations of the problem.**  
> **Search = the process of exploring those possibilities to find a solution.**

The formulation determines what the search algorithm can see. A poor representation can make a simple problem unnecessarily difficult, while a good abstraction can reduce a huge real-world problem to a manageable search space.
## 4. Knowledge Representation and Reasoning
## 5. Planning
## 6. Constraint Satisfaction Problem
## 7. Local Search and Optimization
## 8. Advesarial Search and Game Playing