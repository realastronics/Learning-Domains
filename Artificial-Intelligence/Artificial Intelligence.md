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
## 2. Intelligent Agents
An **agent** is a system that **perceives its environment through sensors and acts upon that environment through actuators**. Agent is not defined by being human-like but by being able to act without human-intervention.

A thermostat, robot, chess program, self-driving car, and LLM-based system can all be considered agents because they:
- receive information from some environment, 
- process that information,
- and produce actions or outputs.

A **percept** is the information an agent receives from its environment at a particular moment. **Percept Sequence** is the complete order of percepts received over time to the agent. Example: for a self-driving car:
```
Percept → camera image + speed + GPS + radar + other sensor data
Action  → accelerate / brake / steer
```

The **agent function** describes the mapping from the agent's percept history to an action:
```
f : percept sequence → action
```

> **Given everything the agent has perceived so far, what should it do next?**
The agent function is an abstract description of the agent's behavior. An **agent program** is the actual computational implementation of that function.
### 2.1 Rational Agent
An agent is **rational** when it chooses the action expected to maximize its performance measure, given:
- the percept sequence available to it,
- its knowledge,
- the actions it can perform,
- and the uncertainty of the environment.

Rational does **not** mean always successful.

A rational agent can make a wrong decision because it may have incomplete information or an imperfect model of the world.
> **Rationality is about choosing the best action given what the agent knows, not about guaranteeing the best outcome.**
### 2.2 PEAS
To specify an agent's task environment, we use **PEAS**:
- **P — Performance measure:** How is success evaluated?
- **E — Environment:** What world does the agent operate in?
- **A — Actuators:** What actions can it perform?
- **S — Sensors:** What information can it perceive?
**Example: Autonomous taxi**

| Component   | Example                              |
| ----------- | ------------------------------------ |
| Performance | Safety, travel time, comfort, cost   |
| Environment | Roads, traffic, pedestrians, weather |
| Actuators   | Steering, brakes, accelerator        |
| Sensors     | Cameras, GPS, radar, lidar           |

The agent perspective turns AI into a very concrete question:
> **Given what the system can perceive, what action should it take to achieve its objective?**

Search, planning, reasoning, learning, and modern AI models can all be understood as different mechanisms for answering this question.
### 2.3 Task Environments
A **task environment** is the part of the world in which an agent operates and whose state can be affected by the agent's actions. The nature of the environment determines what kind of intelligence the agent needs.

**Important properties of task environments**

1. Fully observable vs. partially observable**
   - **Fully observable:** The agent's sensors provide all information relevant to choosing an action.
   - **Partially observable:** The agent has incomplete information about the current state.
  Example: Chess is largely fully observable; driving is partially observable.

2. **Deterministic vs. stochastic**
   - **Deterministic:** An action has a predictable outcome given the current state.
   - **Stochastic:** The outcome involves uncertainty.
  Example: A calculator is deterministic; a robot moving through a crowded room is stochastic.

3. **Episodic vs. sequential**
   - **Episodic:** Each decision is largely independent of previous decisions.
   - **Sequential:** Current actions affect future states and decisions. 
  Example: Image classification can be episodic; chess is sequential.

4. **Static vs. dynamic**
   - **Static:** The environment does not change while the agent is deciding.
   - **Dynamic:** The environment can change independently of the agent.
  Example: Crossword solving is relatively static; driving is dynamic.

5. **Discrete vs. continuous**
   - **Discrete:** States, actions, or time can be represented as distinct values.
   - **Continuous:** They vary over a continuous range. 
  Example: Chess is discrete; vehicle steering is continuous.

5. **Single-agent vs. multi-agent**
   - **Single-agent:** The outcome depends mainly on the agent's own actions.
   - **Multi-agent:** Other agents also influence the environment and may cooperate or compete.
  Example: Sudoku is single-agent; poker is multi-agent.
  
These properties tell us **what kind of reasoning an agent requires**.

A simple, fully observable, deterministic environment may need very little sophisticated intelligence. A partially observable, stochastic, dynamic, multi-agent environment requires much more.

So before designing an agent, we should ask:
> **What kind of world is the agent operating in?**

That question directly influences its architecture, representation, planning, and decision-making strategy.
## Agent Architectures
An **agent architecture** describes how an agent transforms its percepts and internal information into actions.

The architectures differ mainly in **how much internal knowledge and reasoning the agent uses**.
### 1. Simple Reflex Agent
Acts only on the **current percept** using condition-action rules.

```
Percept → Rule → Action
```
Example:
```
If temperature < 20°C → turn heater on
```

**Strength:** Simple and fast.  
**Limitation:** Cannot handle situations where the current percept does not contain enough information.
### 2. Model-Based Reflex Agent
Maintains an **internal state** that represents aspects of the world that cannot be directly observed.

```
Percept + Internal State
          ↓
     Update State
          ↓
         Rule
          ↓
        Action
```

The internal state acts as a **model of the world**.

Example: A robot may remember that an obstacle was previously detected even though it is currently outside its sensors' view.

This allows the agent to operate in **partially observable environments**.
### 3. Goal-Based Agent
A goal-based agent explicitly considers **what it wants to achieve** and chooses actions that help reach that goal.

```
Current State + Goal
        ↓
   Search / Planning
        ↓
      Action
```

Example:

> Goal: Reach Room B.

The agent considers possible paths and selects actions that eventually reach Room B.

This introduces **planning and search** into the agent.
### 4. Utility-Based Agent
Goals alone may not be enough. Suppose two routes both reach the destination, but one is:
- faster
- safer
- cheaper
- or more comfortable.

A utility-based agent uses a **utility function** to measure how desirable different outcomes are.
```
Possible outcomes
       ↓
  Utility values
       ↓
Choose action with
highest expected utility
```

This becomes particularly important when there is **uncertainty or competing objectives**.

> **Goal:** What outcomes are acceptable?  
> **Utility:** How desirable is each outcome?
### 5. Learning Agent
A learning agent can **improve its behavior from experience** rather than relying entirely on rules designed beforehand.

A standard learning-agent architecture contains:

- **Performance element:** selects actions.
- **Learning element:** improves the performance element.
- **Critic:** evaluates how well the agent is performing.
- **Problem generator:** suggests useful exploratory actions.

```
                 ┌──────────────┐
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

The important shift is:

> **Earlier architectures are primarily designed by us; a learning agent can modify or improve its behavior through experience.**
## The progression

These architectures can be understood as increasing sophistication:

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

Each step addresses a limitation of the previous one:

|Architecture|Adds|
|---|---|
|Simple Reflex|Immediate rule-based response|
|Model-Based|Internal representation of the world|
|Goal-Based|Explicit objectives and planning|
|Utility-Based|Preference between possible outcomes|
|Learning|Ability to improve from experience|

The key idea is not that newer architectures always replace older ones. **Modern AI systems often combine several of these ideas.** A system may have an internal model, pursue goals, optimize utility, and learn from experience simultaneously.

### Core mental model

> **Agent architecture is essentially the machinery between perception and action: how an agent represents the world, evaluates possibilities, and decides what to do.

### Expert Systems

An **expert system** is an AI system designed to solve problems in a specific domain by combining **stored domain knowledge** with an **inference mechanism**.

The central idea is:

> **Separate what the system knows from how it reasons with that knowledge.**

### Architecture

```
User / Environment
        ↓
   User Interface
        ↓
   Inference Engine
        ↕
   Knowledge Base
        ↓
      Output
```

**Knowledge Base**  
Contains domain-specific knowledge, often represented as facts and rules.

```
Fact: Patient has a fever.
Rule: IF fever AND cough → possible infection.
```

**Inference Engine**  
Applies the rules to known facts to derive new conclusions.

**User Interface**  
Allows users to provide information and receive conclusions or recommendations.

### Example

A medical expert system might contain:

```
Fever + Cough → Possible respiratory infection
Respiratory infection + Test result → Diagnosis
```

Given a patient's symptoms, the inference engine applies the relevant rules and produces a conclusion.

### Why expert systems mattered

Expert systems were an early demonstration that intelligent behavior could be produced by **explicitly representing knowledge and reasoning over it**, rather than encoding every possible situation as a fixed procedure.

They were particularly useful in narrow domains such as diagnosis, configuration, and troubleshooting.

### Limitations

Their major weakness is that the system depends heavily on the quality and completeness of its knowledge base.

They struggle when:

- knowledge is difficult to express as explicit rules,
- situations are uncertain or novel,
- the number of rules becomes very large,
- or knowledge must be continuously updated.

This is one reason modern AI increasingly relies on **learning from data** rather than requiring humans to explicitly encode all relevant knowledge.

> **Expert systems = explicit knowledge + inference rules + reasoning mechanism.**

With this, the **Intelligent Agents** portion is complete enough for our purposes.
## 3. Problem Solving and Search
## 4. Knowledge Representation and Reasoning
## 5. Planning
## 6. Constraint Satisfaction Problem
## 7. Local Search and Optimization
## 8. Advesarial Search and Game Playing