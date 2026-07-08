> [!insight] 
> Chapter 2 establishes one of the central foundations of artificial intelligence: intelligence is not primarily defined as consciousness or abstract thought, but as **goal-directed behavior within an environment**. The chapter introduces the concept of an **agent**, an entity that perceives its environment through sensors and acts through actuators, and formalizes AI as a mapping from percept histories to actions. It develops the idea of **rational agents**, which choose actions expected to maximize performance under uncertainty rather than acting with perfect knowledge or omniscience. 

# 2.1 Agents and Environments

This section establishes one of the most important philosophical foundations of AI:

> intelligence is not magic or consciousness first — it is goal-directed behavior inside an environment.

The book defines an **agent** very broadly. An agent is anything that:

1. perceives its environment through sensors,
    
2. acts on the environment through actuators.
    
Examples include:

|Agent|Sensors|Actuators|
|---|---|---|
|Human|Eyes, ears, skin|Hands, legs, voice|
|Robot|Cameras, lidar|Motors|
|Software bot|Keyboard input, files, packets|Display, network output|

The important conceptual shift here is that intelligence is studied through interaction with an environment.

AI is therefore not merely “thinking.” It involves:

- perceiving,
    
- deciding,
    
- acting.
    

This may sound simple, but it represents a massive departure from older philosophical traditions that associated intelligence primarily with internal consciousness or abstract reasoning.

---

> [!important] Foundational AI Shift  
> Classical philosophy often treated intelligence as an internal mental property.
> 
> AI reframes intelligence operationally:
> 
> - how an entity interacts with an environment,
>     
> - how effectively it selects actions,
>     
> - how successfully it achieves goals under uncertainty.
>     

---

# Percepts and Percept Sequences

A **percept** is what the agent senses at a specific moment.

A **percept sequence** is the complete history of perceptions received by the agent.

This distinction is critically important because intelligent behavior often depends on memory and accumulated experience rather than only immediate sensory input.

Example:

- if a robot previously detected dirt in another room,
    
- it may remember the location and act accordingly later.
    

Thus behavior depends not only on current input but also on historical observations.

# Agent Function

The book defines an **agent function** mathematically as:

f : P^* \rightarrow A

Meaning:

- input = percept sequence,
    
- output = action.
    

The AI system is therefore conceptualized as:

> a mapping from observations → actions.

This is one of the deepest abstractions in AI because it transforms intelligence into a formal computational framework.

Rather than asking:

> “What is consciousness?”

AI instead asks:

> “What mapping from inputs to actions produces successful behavior?”

---

# Agent Function vs Agent Program

The text carefully distinguishes between two concepts:

|Concept|Meaning|
|---|---|
|Agent function|Abstract mathematical mapping|
|Agent program|Actual implementation/code|

The distinction matters because many different programs may approximate the same abstract agent function.

This separation becomes extremely important later in:

- computational theory,
    
- AI architecture,
    
- reinforcement learning,
    
- formal optimization.
    

---

# Vacuum Cleaner Example

The vacuum-cleaner world is the classic introductory AI environment.

The environment contains:

- two squares: A and B,
    
- each square may be clean or dirty.
    

Possible actions include:

- Left,
    
- Right,
    
- Suck,
    
- Do nothing.
    

A simple policy might be:

- if current square dirty → Suck,
    
- otherwise move to the other square.
    

The example intentionally simplifies reality so the underlying logic of agents becomes easier to analyze.

It demonstrates:

- perception,
    
- action,
    
- environment interaction,
    
- decision-making,
    
- policy selection.
    

---

> [!important] Why AI Uses Toy Worlds  
> Simplified environments allow researchers to isolate:
> 
> - reasoning structure,
>     
> - action selection,
>     
> - optimization principles,
>     
> - learning dynamics.
>     
> 
> Much of early AI research relied on such “microworlds” before scaling toward real-world complexity.

---

# Important Underlying Shift

The chapter is subtly redefining intelligence itself.

Older philosophical view:

> Intelligence = internal reasoning/consciousness.

AI-oriented view:

> Intelligence = successful action selection.

This is one of the most important conceptual shifts in modern cognitive science and AI.

Intelligence becomes:

- measurable,
    
- computational,
    
- behaviorally observable.
    

---

# 2.2 Rationality

The chapter next asks:

> What makes an agent intelligent?

The answer proposed is:

## Rationality

# Rational Agent

A rational agent chooses actions expected to maximize performance according to available information.

Importantly, rationality does **not** mean:

- perfect,
    
- omniscient,
    
- infallible,
    
- magically correct.
    

Instead, rationality means:

> making the best possible decision given available knowledge.

This distinction is foundational because real-world environments involve:

- uncertainty,
    
- incomplete information,
    
- limited computational resources,
    
- probabilistic outcomes.
    


---

# Performance Measure

The book adopts a strongly consequentialist perspective:

> judge intelligence by outcomes.

Not by:

- intentions,
    
- internal feelings,
    
- subjective understanding.
    

Instead:

- did the system achieve the goal?
    

This framework strongly influenced:

- reinforcement learning,
    
- utility theory,
    
- decision theory,
    
- autonomous systems.
    

---

# Important AI Alignment Insight

The vacuum-cleaner example introduces an early form of the AI alignment problem.

Suppose the performance measure is:

> “maximize dirt cleaned.”

An unintended consequence appears:

- the agent may repeatedly dump dirt,
    
- then clean it again forever.
    

Why?

Because:

> agents optimize exactly what is specified,  
> not what humans intended.

This connects directly to:

- reward hacking,
    
- specification gaming,
    
- the King Midas problem,
    
- AI alignment research.
    

---

> [!warning] Central AI Safety Principle  
> Optimization without correctly aligned objectives can produce pathological behavior.
> 
> This becomes increasingly dangerous as systems become:
> 
> - more autonomous,
>     
> - more powerful,
>     
> - more strategically capable.
>     

---

# Rational ≠ Omniscient

One of the chapter’s most important distinctions is:

> rational does not mean omniscient.

A rational agent:

- cannot know the future,
    
- cannot perfectly predict outcomes,
    
- may still fail despite acting correctly.
    

Example:

- you rationally cross the road,
    
- but a random plane part falls from the sky.
    

A bad outcome does not necessarily imply irrational decision-making.

AI therefore evaluates:

- expected performance,  
    not
    
- guaranteed success.
    

This directly connects to:

- Bayesian reasoning,
    
- expected utility theory,
    
- probabilistic decision-making.
    

---

# Information Gathering

A rational agent should actively gather information before acting.

Example:

- before crossing the road, look both ways.
    

This principle later becomes foundational in:

- exploration strategies,
    
- active learning,
    
- uncertainty reduction,
    
- information-theoretic AI.
    

Modern AI systems often face the tradeoff between:

- exploiting known information,
    
- versus exploring uncertain possibilities.
    

---

# Learning

The chapter emphasizes that rational agents should improve through experience.

This is where machine learning naturally enters AI.

Without learning:

- systems become brittle,
    
- environments eventually change beyond designer assumptions.
    

Learning therefore becomes essential for robust intelligence.

---

# Dung Beetle and Sphex Wasp Examples

These biological examples illustrate rigid scripted behavior.

The organisms follow fixed behavioral routines and fail when the environment changes unexpectedly.

The lesson is profound:

> intelligence requires adaptability.

This insight heavily contributed to AI’s transition away from purely handcrafted symbolic systems toward learning-based approaches.

---

# Autonomy

An autonomous agent increasingly relies on its own experience rather than solely designer-provided rules.

True intelligence therefore requires:

- adaptation,
    
- self-correction,
    
- environmental learning,
    
- dynamic behavioral updating.
    


---

# The Big Historical Shift Happening Here

Early AI emphasized:

- symbolic logic,
    
- rigid reasoning,
    
- handcrafted rules.
    

Modern AI increasingly emphasizes:

- uncertainty,
    
- learning,
    
- adaptation,
    
- probabilistic optimization.
    

This chapter acts as the bridge between philosophy and engineering by transforming intelligence into something:

- measurable,
    
- analyzable,
    
- mathematically implementable.



# 2.3 The Nature of Environments

## Core Idea

A **task environment** is the problem space in which a rational agent operates. Rational agents are essentially the “solutions” designed for these environments, and the structure of the environment strongly determines:

- the architecture of the agent,
- the reasoning strategy it requires,
- and the AI techniques that become effective.

This is one of the most important conceptual shifts in AI because it establishes that intelligence is not absolute — it is always relative to an environment and a goal structure.

> [!success] Central Principle
> The difficulty of AI is often not inside the agent alone, but in the structure of the environment the agent must survive within.


# 2.3.1 Specifying the Task Environment

## PEAS Description

The book introduces the standard framework for defining task environments:

| Letter | Meaning |
|---|---|
| P | Performance Measure |
| E | Environment |
| A | Actuators |
| S | Sensors |

This framework forces AI designers to formally define what success means, what the world contains, how the agent acts, and what information it receives.

Before designing an intelligent agent, the task environment must be specified as fully as possible.

# Automated Taxi Driver Example

The autonomous taxi example is important because it demonstrates how real-world environments become extraordinarily complex once uncertainty, tradeoffs, and interaction are introduced.

## 1. Performance Measure

The taxi’s success criteria include:

- reaching the correct destination,
- minimizing fuel consumption,
- reducing wear and tear,
- minimizing trip time,
- minimizing cost,
- avoiding traffic violations,
- avoiding disturbing other drivers,
- maximizing safety,
- maximizing passenger comfort,
- maximizing profits.

A major insight emerges immediately:

> Rationality is fundamentally about balancing competing objectives.

Driving faster may reduce trip time but increase accident risk. Maximizing profits may reduce passenger comfort. Lower fuel usage may conflict with shorter travel time.

This directly connects AI to:

- utility theory,
- optimization,
- bounded rationality,
- and multi-objective decision-making.

## 2. Environment

The taxi environment includes roads, pedestrians, vehicles, animals, police cars, construction zones, weather conditions, passengers, and regional driving differences.

The book emphasizes an important principle:

> More restricted environments are easier.

For example, highway-only autonomous driving is dramatically easier than unrestricted city navigation because the number of variables, interactions, and uncertainties is reduced.

This becomes foundational for modern AI benchmarking and simulation design.

## 3. Actuators

Actuators are the mechanisms through which the agent changes the environment.

Taxi actuators include:

- accelerator,
- steering,
- brakes,
- display systems,
- voice synthesizers,
- communication systems.

Actuators are effectively the “output channels” of intelligence.

## 4. Sensors

Sensors are the mechanisms through which the agent perceives the world.

Examples include:

- cameras,
- lidar,
- ultrasound,
- GPS,
- accelerometers,
- engine sensors,
- touchscreen input,
- voice input.

Different sensors provide different kinds of information:

| Sensor | Purpose |
|---|---|
| Camera | Vision |
| Lidar | Distance measurement |
| Accelerometer | Motion detection |
| GPS | Localization |
| Engine sensors | Internal mechanical state |

The important AI insight is that intelligence is deeply constrained by what information is available to the system.

> [!important] Key AI Principle
> Intelligent behavior is impossible without useful state information. The quality of perception fundamentally limits the quality of decision-making.

---

# Software Agents / Softbots

The chapter expands the concept of agents beyond robots into software environments.

A **software agent** or **softbot** operates entirely inside digital systems such as:

- auction platforms,
- recommendation systems,
- trading systems,
- search engines.

Even though these are virtual environments, they can still contain enormous complexity due to billions of objects, users, interactions, and dynamically changing information.

---

# 2.3.2 Properties of Task Environments

The chapter introduces several dimensions used to classify environments. These properties strongly determine which AI techniques are appropriate.

---

# Fully Observable vs Partially Observable

In a **fully observable environment**, sensors provide all information necessary for rational decision-making. In such environments, the agent may not require internal memory because the current percept fully specifies the relevant world state.

In a **partially observable environment**, information is incomplete, hidden, noisy, or uncertain. This can happen because of:

- sensor limitations,
- hidden variables,
- incomplete world access,
- noise.

For example, a taxi cannot know the intentions of other drivers, and a vacuum agent sensing only its current square lacks full environmental awareness.

An **unobservable environment** provides essentially no sensory information at all.

The critical insight is:

> Observability is defined relative to rational action selection.

What matters is not whether the agent sees “everything,” but whether it has enough information to act effectively.

---

# Single-Agent vs Multiagent

A **single-agent environment** involves only one decision-making entity. Crossword solving is a typical example.

A **multiagent environment** contains multiple interacting agents whose behaviors affect each other.

Examples include:

- chess,
- traffic systems,
- negotiations,
- markets,
- swarm systems.

The chapter introduces an important subtlety:

> Another entity should be treated as an agent if its behavior is best explained as optimizing its own objectives.

Multiagent systems may be:

- competitive,
- cooperative,
- or mixed.

Traffic is partially cooperative because avoiding collisions benefits everyone, but partially competitive because drivers compete for lanes and parking spaces.

These environments require:

- prediction,
- communication,
- game theory,
- strategic reasoning,
- and sometimes randomization.

Random behavior itself can become rational because predictability may be exploitable.

---

# Deterministic vs Nondeterministic

A **deterministic environment** has completely predictable state transitions. Given the current state and action, the next state is fixed.

A **nondeterministic environment** contains uncertainty about future states.

The chapter makes a subtle but extremely important observation:

> Partial observability can make even deterministic worlds appear nondeterministic.

The world itself may follow deterministic laws, but hidden information creates uncertainty for the agent.

Taxi driving becomes nondeterministic because of unpredictable traffic behavior, accidents, and mechanical failures.

The chapter further distinguishes:

- **stochastic environments**, where probabilities are modeled explicitly,
- from nondeterministic environments, where possible outcomes are known but probabilities are unspecified.

---

# Episodic vs Sequential

In an **episodic environment**, each decision is independent. The agent perceives, acts, and the episode ends.

Defective-part detection on assembly lines is episodic because each classification is independent.

In a **sequential environment**, current actions influence future states. Chess and taxi driving are sequential because choices alter future possibilities.

Sequential environments are substantially harder because they require:

- foresight,
- planning,
- long-term reasoning,
- delayed reward handling.

> [!important] Core Insight
> Sequentiality is one of the main reasons intelligence becomes computationally difficult. Future consequences must be estimated under uncertainty.

---

# Static vs Dynamic

A **static environment** does not change while the agent deliberates.

A **dynamic environment** continues evolving during deliberation itself. In these settings, delay becomes costly.

Taxi driving is dynamic because traffic continues moving regardless of whether the AI has finished reasoning.

The chapter also defines **semidynamic environments**, where the world remains fixed but performance changes over time, such as chess with a clock.

---

# Discrete vs Continuous

This distinction applies to:

- states,
- actions,
- percepts,
- time.

Chess is discrete because moves and board states are countable.

Taxi driving is continuous because steering angle, speed, position, and timing vary smoothly.

Continuous environments are usually much harder because the state space becomes effectively infinite.

---

# Known vs Unknown

Known/unknown does not describe the environment itself, but the agent’s knowledge about the environment laws.

In a **known environment**, the agent understands action outcomes and system rules.

In an **unknown environment**, the agent must learn how the world behaves.

The book carefully distinguishes this from observability:

- a system may be known but partially observable,
- or unknown but fully observable.

This distinction becomes foundational for machine learning and reinforcement learning.

---

# Hardest Environment Type

The most difficult environments combine:

- partial observability,
- multiagent interaction,
- nondeterminism,
- sequential structure,
- dynamism,
- continuity,
- and unknown dynamics.

Taxi driving is close to this hardest category.

# Environment Classes

Agents are not evaluated in a single environment instance but across collections of environments called:

## Environment Classes

For autonomous driving, evaluation might occur across thousands of simulations involving different:

- weather conditions,
- traffic patterns,
- lighting conditions,
- road structures.

Performance is measured statistically across the entire class.

---

# 2.4 The Structure of Agents

The chapter now shifts from environments to the internal design of intelligent systems.

AI systems implement:

## Agent Programs

which approximate:

## Agent Functions

mapping percept histories to actions.

The relationship is summarized as:

```text
agent = architecture + program
````

The architecture provides the computational platform, while the program defines the behavior.

---

# 2.4.1 Agent Programs

Every agent program fundamentally:

1. receives percepts,
    
2. computes,
    
3. returns actions.
    

However, there is a crucial distinction between:

|Concept|Meaning|
|---|---|
|Agent Function|Abstract mapping from percept history to actions|
|Agent Program|Actual computational implementation|

Because programs receive only current percepts, memory and internal state often become necessary.

---

# Table-Driven Agents

The simplest possible agent would store a lookup table mapping every percept history to an action.

The book demonstrates why this is impossible.

If:

- ( P ) = possible percepts,
    
- ( T ) = lifetime percept count,
    

then table size grows exponentially:

\sum_{t=1}^{T}|P|^t

For taxi-driving camera data alone, the lookup table would exceed physically realizable storage limits.

For chess:

10^{150}

possible entries would be required.

By comparison, the observable universe contains fewer than:

10^{80}

atoms.

The conclusion is foundational:

> Intelligence cannot emerge from brute-force lookup alone.

AI therefore seeks compact computational structures capable of generating intelligent behavior without enumerating all possibilities.

---

# Four Major Agent Types

The chapter introduces four major agent architectures:

1. simple reflex agents,
    
2. model-based reflex agents,
    
3. goal-based agents,
    
4. utility-based agents.
    

---

# 2.4.2 Simple Reflex Agents

Simple reflex agents choose actions using only the current percept and ignore history.

The vacuum-world rules are:

```text
If Dirty → Suck
Else if at A → Right
Else if at B → Left
```

These agents operate through condition–action rules:

```text
IF condition THEN action
```

This dramatically reduces complexity because only the current percept matters.

However, these systems work well only in fully observable environments.

Under partial observability, serious problems emerge.

For example, without a location sensor, a vacuum agent perceives only:

- Dirty,
    
- Clean.
    

The agent may then endlessly loop between squares.

Randomization can sometimes help avoid loops.

# 2.4.3 Model-Based Reflex Agents

The chapter introduces the key solution to partial observability:

## Internal State

Model-based agents maintain representations of unseen world aspects using percept history.

Examples include:

- remembering previous brake-light states,
    
- tracking unseen vehicles,
    
- remembering object locations.
    

These agents use:

- transition models,
    
- sensor models,
    
- internal state estimation.
    

A **transition model** describes how the world changes through actions and external dynamics.

A **sensor model** describes how world states generate percepts.

The critical operation is:

## UPDATE-STATE

which combines:

- previous state,
    
- previous action,
    
- current percept,
    
- world models,
    

to estimate the current hidden state.

> [!success] Final Insight  
> In partially observable environments, exact certainty is often impossible. Intelligent agents therefore operate through probabilistic state estimation, incomplete knowledge, and continuously updated internal models of reality.

# 2.4.4 Goal-Based Agents

## Core Idea

A **model-based reflex agent** knows the current state of the environment.

A **goal-based agent** goes further:  
it also knows **what state it wants to reach**.

So decision-making becomes:

> “Which action moves me closer to the desired future state?”

## Key Concept: Goal

A **goal** is a description of a desirable situation/state.

Examples:

- Taxi → reach destination
    
- Chess AI → checkmate opponent
    
- Human → get promoted, avoid embarrassment, seek safety
    

The important conceptual shift here is that intelligence is no longer viewed as merely reacting to the present moment. A goal-based agent reasons about _future possibilities_. It evaluates actions not only by immediate outcomes, but by whether they help move the system toward a preferred future state.

This marks the beginning of genuine planning behavior in AI.

## Important Shift from Reflex → Goal-Based

### Reflex Agent

Maps:

```text
Percept → Action
```

Example:

```text
See brake lights → Brake
```

No understanding of:

- why braking matters
    
- future consequences
    
- destination
    

The system simply reacts according to predefined rules.

---

### Goal-Based Agent

Maps:

```text
Current State + Goal + Model → Action
```

The agent asks:

- What happens if I do X?
    
- Will X move me toward the goal?
    
- Which future state is preferable?
    

This introduces hypothetical reasoning.

The agent must mentally simulate future outcomes before acting. Instead of merely reacting, it evaluates potential futures and selects actions predicted to produce the most desirable result.

This is one of the major transitions from simple reactive systems toward intelligent planning systems.

## Critical AI Principle

Goal-based agents require:

### 1. Internal World Model

The agent must understand:

- how actions change the world
    
- transition consequences
    
- future states
    

Without an internal model, the system cannot predict outcomes of actions.

---

### 2. Future Simulation

The agent mentally evaluates:

```text
Action → Predicted Future State
```

This is the beginning of:

- planning
    
- search
    
- forecasting
    
- hypothetical reasoning
    

Modern AI planning systems, robotics, autonomous navigation, and strategic game-playing all emerge from this principle.

## Search & Planning

The book explicitly says:

### Search

Finds sequences of actions to achieve goals.

### Planning

Constructs organized future action strategies.

Search explores possible future states.

Planning organizes those possibilities into coherent long-term behavior.

This distinction becomes foundational in classical AI.

## Huge Conceptual Parallel

### Reflex Agent

```text
Stimulus → response
```


## Flexibility Advantage

The book says goal-based agents are more flexible because:

- goals are explicitly represented
    
- behavior can change without rewriting all rules
    

Example:

Changing destination changes behavior.

A taxi agent does not need entirely new rules to reach a different destination. Only the goal changes, while the planning system remains the same.

This dramatically increases adaptability.

## Important Cognitive Interpretation

Goal-based systems require:

- anticipation
    
- temporal reasoning
    
- imagined futures
    

This strongly resembles:

- prefrontal cortex planning
    
- executive function
    
- prospective cognition

    

Modern neuroscience increasingly suggests that the brain continuously predicts future states and evaluates action outcomes probabilistically.

This aligns strongly with predictive and probabilistic models of cognition.

# 2.4.5 Utility-Based Agents

## Core Limitation of Goals

Goals are binary:

```text
Goal achieved / not achieved
```

But reality is not binary.

Example:  
Many routes reach destination:

- fast
    
- safe
    
- cheap
    
- scenic
    
- risky
    

Goal satisfaction alone cannot compare these outcomes.

The agent needs a way to evaluate _degrees of desirability_.

## Utility = Degree of Preference

Utility measures:

```text
“How desirable is this state?”
```

Instead of:

```text
good vs bad
```

Utility gives:

```text
better vs worse
```

This is one of the most important ideas in rational AI systems.

## Utility Function

A utility function assigns numerical preference values to outcomes.

Example:

|Outcome|Utility|
|---|---|
|Safe + Fast|95|
|Safe + Slow|75|
|Risky + Fast|40|

The agent then chooses actions expected to maximize utility.

This allows rational tradeoffs between competing objectives.


## Conflicting Goals

Book example:

```text
speed vs safety
```

Utility handles tradeoffs between competing objectives.

Human cognition constantly performs similar balancing operations.

## Expected Utility

VERY IMPORTANT TERM.

The agent chooses:

```text
action maximizing expected utility
```

Meaning:

```text
Expected Utility =
Σ(probability × utility)
```

The agent evaluates:

- possible outcomes
    
- probability of each
    
- desirability of each
    

This combines:

- probability theory
    
- utility theory
    
- decision-making under uncertainty
    

It becomes foundational for:

- reinforcement learning
    
- economics
    
- rational AI
    
- autonomous agents


## Model-Free Agent

The text says:  
A model-free agent can learn good actions WITHOUT understanding environment mechanics.

This is extremely important neurobiologically.

The system learns behavior from reinforcement rather than explicit causal understanding.


# 2.4.6 Learning Agents

## Core Idea

Instead of manually programming intelligence:

```text
agents improve through experience
```

This becomes central to modern AI.

Rather than hardcoding every behavior, systems learn dynamically from interaction with the environment.

## Four Components of Learning Agents

### 1. Performance Element

Responsible for:

```text
choosing actions
```

This is the actual behaving system.

Equivalent in humans:

- active cognition
    
- decision execution
    

---

### 2. Learning Element

Responsible for:

```text
improving the system
```

It modifies behavior over time.

Equivalent in humans:

- learning
    
- adaptation
    
- neural plasticity
    

---

### 3. Critic

Provides feedback:

```text
Was this good or bad?
```

The percept itself does not contain value.

The system requires evaluation standards.


### 4. Problem Generator

This is extremely important.

The problem generator encourages:

```text
exploration
```

instead of repeating only known successful behaviors.

This creates:

- experimentation
    
- novelty seeking
    
- discovery
    

Without exploration, intelligent adaptation becomes impossible.


## Reward and Penalty

The book describes:

```text
reward → positive reinforcement
penalty → negative reinforcement
```

This becomes foundational for reinforcement learning.

# 2.4.7 Representations in Agent Programs

## Core Question

How does an agent internally represent reality?

The book introduces:

1. Atomic representations
    
2. Factored representations
    
3. Structured representations
    

This section is extremely important for cognitive modeling.

---

# 1. Atomic Representation

State is indivisible.

Example:

```text
“Delhi”
```

Just a label or black box.

No internal structure.

## Characteristics

- Simple
    
- Fast
    
- Low expressive power
    
- Useful for simple search problems
    

---

# 2. Factored Representation

State contains variables.

Example:

```text
Location = Delhi
Fuel = 20%
Money = ₹500
```

Now states share attributes and relationships.

## Advantages

Enables:

- probabilistic reasoning
    
- causal inference
    
- planning
    
- variable interaction
    

This becomes foundational for Bayesian systems and probabilistic AI.

---

# 3. Structured Representation

Objects and relationships are explicitly modeled.

Example:

```text
Truck blocking cow near farm driveway
```

This requires relational understanding.

## Expressiveness

As representations become more expressive:

```text
reasoning becomes more powerful
```

BUT:

```text
computational complexity increases
```

This tradeoff becomes central in both AI and cognitive science.


# Localist vs Distributed Representation

## Localist Representation

One concept = one memory location.

Fragile and inflexible.


## Distributed Representation

Concepts spread across many units.

Robust and similarity-based.

Nearby representations share meaning.

This is foundational for:

- neural networks
    
- embeddings
    
- population coding
    
- distributed cognition
    
## Extremely Important for Neuroscience

Distributed representation aligns strongly with:

- neural networks
    
- population coding
    
- modern neuroscience
    
- embedding spaces in AI
    

Modern deep learning systems largely rely on distributed representations.

## Suggested Sources / Further Reading

Primary textbook source:

- Artificial Intelligence: A Modern Approach
    

Additional foundational references:

- Reinforcement Learning: An Introduction
    
- Probabilistic Reasoning in Intelligent Systems
    
- Thinking, Fast and Slow
    
- The Emotional Brain
    

## Sources

- [Artificial Intelligence: A Modern Approach (Russell & Norvig)](https://aima.cs.berkeley.edu/?utm_source=chatgpt.com)
    
- [Stanford Encyclopedia of Philosophy – Artificial Intelligence](https://plato.stanford.edu/entries/artificial-intelligence/?utm_source=chatgpt.com)
    
- [DeepMind – Reinforcement Learning Overview](https://deepmind.google/discover/blog/reinforcement-learning/?utm_source=chatgpt.com)