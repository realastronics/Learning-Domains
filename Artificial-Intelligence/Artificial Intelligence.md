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
An **agent** is a system that **perceives its environment through sensors and acts upon that environment through actuators**. Agent is not defined by being human-like or even by being complex.

A thermostat, robot, chess program, self-driving car, and LLM-based system can all be considered agents because they:
- receive information from some environment, 
- process that information,
- and produce actions or outputs.
### Percept
A **percept** is the information an agent receives from its environment at a particular moment.

The complete sequence of percepts received over time is the **percept sequence**.

For a self-driving car:
```
Percept → camera image + speed + GPS + radar + other sensor data
Action  → accelerate / brake / steer
```

Agent function
The **agent function** describes the mapping from the agent's percept history to an action:

```
f : percept sequence → action
```

In other words:

> **Given everything the agent has perceived so far, what should it do next?**

The agent function is an abstract description of the agent's behavior. An **agent program** is the actual computational implementation of that function.

### Rational Agent
An agent is **rational** when it chooses the action expected to maximize its performance measure, given:

- the percept sequence available to it,
    
- its knowledge,
    
- the actions it can perform,
    
- and the uncertainty of the environment.
    
Rational does **not** mean always successful.

A rational agent can make a wrong decision because it may have incomplete information or an imperfect model of the world.

> **Rationality is about choosing the best action given what the agent knows, not about guaranteeing the best outcome.**
### PEAS
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
### The central idea
The agent perspective turns AI into a very concrete question:

> **Given what the system can perceive, what action should it take to achieve its objective?**

Search, planning, reasoning, learning, and modern AI models can all be understood as different mechanisms for answering this question.
## 3. Problem Formulation
## 4. Search
## 5. Local Search & Optimization
## 6. Adversarial Search & Games
## 7. Constraint Satisfaction Problem
## 8. Planning