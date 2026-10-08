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
An **agent** is a system that **perceives its environment through sensors and acts upon it through actuators**. 

The important idea is not that an agent must be human-like, but that it can **use percepts to select actions** in an environment. A thermostat, robot, chess program, or autonomous vehicle can be an agent because it receives information, processes it, and produces actions or outputs.

**Percept** is the information an agent receives from its environment at a particular moment. **Percept sequence** is the complete history of percepts received by the agent.
```
Percept → camera image + speed + GPS + radar
Action  → accelerate / brake / steer
```

The **agent function** specifies the mapping from the percept sequence to an action:
*f : percept sequence → action*
The **agent program** is the actual computational implementation of the agent function.

**Rational agent** is an agent that chooses the action expected to **maximize its performance measure**, given its percept sequence, available knowledge, available actions, and the uncertainty of the environment.
> **Rationality means choosing the best action justified by the information available, not guaranteeing a successful outcome.**

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

There are many kinds of agent architectures as we have noted below:

**Simple Reflex Agent -** It uses direct condition-action rules based only on the **current percept** . It's simple and fast, but ineffective when the current percept alone is insufficient to determine the appropriate action. 
	(*Percept → Rule → Action*)

**Model-Based Reflex Agent -** It maintains an **internal state** that represents aspects of the world that may not be directly observable. The internal state acts as a model of how the world changes. This allows the agent to function in **partially observable environments**.
	*Percept + Previous State → Update Internal State → Rule → Action*

**Goal-Based Agent -** It chooses actions by considering a desired **goal state**. The agent considers possible sequences of actions and selects one that achieves the goal.
	Current State + Goal → Search/Planning → Action

**Utility-Based Agent -** In goal based, the goals tell an agent whether an outcome is acceptable, but not necessarily **which acceptable outcome is better**. Here, A utility function assigns a measure of desirability to outcomes, based on which actions are taken. This approach becomes especially important when outcomes are uncertain or objectives compete.
	Possible outcomes → Utility Values → Choose action with highest expected utility

**Learning Agent -** A learning agent improves its behavior through **experience** rather than relying entirely on knowledge and rules specified beforehand.

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
## 2.3) Expert Systems
An **expert system** is an AI system designed to solve problems in a specific domain by **combining explicit domain knowledge with an inference mechanism**. The central idea is:
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
A **problem formulation** is a formal description of a problem that specifies what the agent is trying to achieve and the possible actions it can take to get there. The purpose is to convert a real-world objective into a representation that a search algorithm can solve.

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
## 3.2) Search Trees & State-Space Graphs
Once a problem has been formulated, the agent needs a way to **explore the possible states** to find a solution. Two related representations are important: the **state-space graph** and the **search tree**.

**State-space graph** represents the actual problem:

- **Nodes** represent states.
- **Edges** represent actions that move from one state to another.
- It shows which states are actually connected by the problem's rules.

```
A ── B ── C
│    │
D ── E
```

Here, `A, B, C, D, E` are states and the edges represent possible actions.

**Search tree** represents the **process of exploring the state space** from a particular initial state.

The root is the initial state, and each branch represents an action sequence.

```
        A
      /   \
     B     D
    / \     \
   C   E     F
```

The crucial distinction is:
> **State-space graph describes the problem; search tree describes the exploration of that problem.**

A search tree may contain the **same state multiple times** because different action sequences can reach the same state.

For example:
```
        A
       / \
      B   C
       \ /
        D
```

`D` is one state in the state-space graph, but a search tree could contain two copies of `D`:
```
        A
       / \
      B   C
       \ /
        D
```

This distinction matters because repeated states can cause **redundant work and even infinite loops** during search. Search algorithms therefore often maintain an **explored/visited set** to avoid repeatedly expanding states they have already encountered.

### Core mental model

```
Problem formulation
        ↓
   State-space
        ↓
     Search
        ↓
 Explore possible paths
        ↓
      Solution
```

> **State = where the agent can be.**  
> **Action = how it moves.**  
> **State space = all reachable possibilities.**  
> **Search tree = the possibilities explored by the algorithm.**

This distinction becomes essential when we compare **BFS, DFS, Uniform-Cost Search, and A***.
## 3.3) Uninformed Search
**Uninformed search** explores the state space without using domain-specific knowledge about how close a state is to a goal. It uses only the problem formulation: **initial state, actions, transition model, goal test, and path cost**. The central question is:

> **Which unexpanded node should be explored next?**

A search procedure maintains a **frontier** of generated but unexpanded nodes. When a node is expanded, its successors are generated and added to the frontier according to the strategy being used. In graph search, an **explored set** is also maintained to avoid repeatedly expanding the same state.
#### Breadth-First Search (BFS)
BFS expands the **shallowest node first**, exploring the search tree level by level. It uses a **FIFO queue**.

```
        A
      / | \
     B  C  D
    / \
   E   F

Expansion: A → B → C → D → E → F
```

BFS is appropriate when **solution depth** is the main concern. With equal step costs, the shallowest solution is also the cheapest.
- **Complete:** Yes, if the branching factor is finite.
- **Optimal:** Yes, when all step costs are equal.
- **Time:** O(b^d)
- **Space:** O(b^d)
where `b` is the branching factor and `d` is the depth of the shallowest goal.

**Key idea:** BFS minimizes **number of actions**, not general path cost.
#### Uniform-Cost Search (UCS)
BFS treats every step as having the same cost. **Uniform-Cost Search** instead expands the node with the **lowest path cost from the initial state**.
$$f(n)=g(n)$$
where `g(n)` is the actual cost of the path from the initial state to node `n`.

UCS uses a **priority queue** ordered by `g(n)`.
```
A → B → Goal      cost = 10
A → C → D → Goal  cost = 7
```
UCS chooses the second path even though it is deeper, because its total cost is lower.

- **Complete:** Yes, if every step cost is at least some positive constant varepsilon > 0.
- **Optimal:** Yes, under the same condition.
- **Time/Space:** Can be exponential in the optimal solution cost; commonly expressed as $$O\left(b^{1+\lfloor C^*/\varepsilon \rfloor}\right)$$, where `C*` is the optimal solution cost.

**Key idea:** UCS minimizes **path cost**, whereas BFS minimizes **depth**.
#### Depth-First Search (DFS)
DFS expands the **deepest unexpanded node first**, following one branch as far as possible before backtracking. It uses a **LIFO stack**.
```
        A
       / \
      B   C
     / \
    D   E

Expansion: A → B → D → E → C
```
Its major advantage is memory efficiency; its major weakness is that it can spend a very long time following an unproductive branch.
- **Complete:** No, in general; it may follow an infinite path or become trapped in cycles.
- **Optimal:** No.
- **Time:** O(b^m)
- **Space:** O(bm)
where `m` is the maximum depth of the search tree.

**Key idea:** DFS prioritizes **depth over solution quality**.
#### Depth-Limited Search (DLS)
DLS is DFS with a predetermined **depth limit** `l`. Nodes at depth `l` are not expanded. This prevents DFS from descending indefinitely, but introduces a new failure mode: a valid solution deeper than the limit will not be found.
- **Complete:** Only if l \geq d, assuming finite branching.
- **Optimal:** No, in general.
- **Time:** O(b^l)
- **Space:** O(bl)

**Key idea:** DLS trades unrestricted depth for a controlled search boundary.
#### Iterative Deepening Search (IDS)
IDS repeatedly performs depth-limited search with increasing limits:
```
Depth 0
   ↓
Depth 1
   ↓
Depth 2
   ↓
Depth 3
   ↓
...
```

It combines the **shallow-solution behavior of BFS** with the **low memory requirement of DFS**.
- **Complete:** Yes, for finite branching factor.
- **Optimal:** Yes, when step costs are equal.
- **Time:** O(b^d)
- **Space:** O(bd)

Although shallow nodes are generated repeatedly, most nodes in a tree search occur at the deepest level, so the repeated work is usually acceptable.

**Key idea:** IDS is useful when the solution depth is unknown but memory is limited.
#### Comparison Table

| Strategy | Expands next            | Complete       | Optimal          | Main strength              | Main weakness                |
| -------- | ----------------------- | -------------- | ---------------- | -------------------------- | ---------------------------- |
| **BFS**  | Shallowest node         | Yes            | Yes, equal costs | Finds shallow solutions    | Very high memory             |
| **UCS**  | Lowest $$g(n)$$         | Yes*           | Yes*             | Minimum-cost solution      | Can be expensive             |
| **DFS**  | Deepest node            | No, in general | No               | Very low memory            | Can get lost in bad branches |
| **DLS**  | Deepest within limit    | If $$l\ge d$$  | No               | Prevents infinite depth    | Requires a suitable limit    |
| **IDS**  | Increasing depth limits | Yes            | Yes, equal costs | BFS-like + DFS-like memory | Repeats shallow work         |
*UCS requires step costs bounded below by a positive constant.

The progression is therefore:
```
BFS
→ "Which solution is shallowest?"

UCS
→ "Which solution costs the least?"

DFS
→ "Which branch can I explore deepest?"

DLS
→ "How deep may I explore?"

IDS
→ "What if I do not know the required depth?"
```

The deeper principle is:
> **Uninformed search does not know which state is closer to the goal. It can only impose a policy for deciding which unexplored possibility to examine next.**

That limitation motivates **informed search**. A heuristic gives the search algorithm additional knowledge about **which states appear more promising**, leading to **Greedy Best-First Search and A(`*`)***.

Add a search-graph notation boxClarify tree-search versus graph-search costs
## 3.4 Informed Search
**Informed search** uses additional problem-specific knowledge to decide which states are more promising. Unlike uninformed search, it does not treat all unexplored states as equally useful.

The key idea is a **heuristic function**. **Heuristic** is an estimate of the remaining cost from a state `n` to a goal.
$$ [ h(n) = \text{estimated cost from } n \text{ to a goal} ] $$
For example, in route finding, the **straight-line distance** from the current city to the destination can be used as a heuristic. It does not tell us the actual road distance, but it gives us useful information about which locations are likely to be closer to the goal.

```
Current state
     ↓
   h(n)
     ↓
Estimated distance to goal
```

The important distinction is:
> **Path cost tells us how much we have already paid.**  
> **Heuristic cost estimates how much remains.**

This gives an informed search algorithm a way to distinguish between alternatives that an uninformed algorithm would treat identically.
### Greedy Best-First Search
**Greedy Best-First Search** selects the node that appears closest to the goal according to the heuristic.

Its evaluation function is:
$$f(n) = h(n)$$
So it asks:
> **Which state looks closest to the goal right now?**

Example:
```
             A
           /   \
         B       C
       h=7      h=3
```
Greedy search chooses `C` because `h(C) < h(B)`.

The advantage is that it can reach a goal quickly when the heuristic is informative.

However, it considers **only the estimated remaining cost** and ignores the cost already incurred.

This can produce poor decisions:
```
Path 1: expensive so far + appears close
Path 2: cheap so far + appears slightly farther
```

Greedy search may choose Path 1 simply because its destination _looks_ closer.

**Completeness:** Not guaranteed in general.
**Optimality:** No.
**Core weakness:** It can be misled by a heuristic because it does not consider the cost already paid.

Uninformed search has no basis for saying:
> "This branch looks more promising than that one."

Informed search introduces that knowledge through a heuristic:
```
Uninformed Search
→ "What can I explore next?"

Informed Search
→ "What can I explore next that looks more promising?"
```
This is the fundamental shift from **blind exploration** to **guided exploration**.

But there is an important trade-off:
> **A heuristic can make search dramatically more efficient, but a misleading heuristic can also lead the search in the wrong direction.**

This leads naturally to **A***, which combines the cost already incurred with the estimated cost remaining:
$$f(n)=g(n)+h(n)$$

where `g(n)` is the actual cost from the initial state to `n`, and `h(n)` estimates the cost from `n` to a goal.
## 4. Knowledge Representation and Reasoning
## 5. Planning
## 6. Constraint Satisfaction Problem
## 7. Local Search and Optimization
## 8. Advesarial Search and Game Playing