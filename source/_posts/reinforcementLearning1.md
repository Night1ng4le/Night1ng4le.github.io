---
title: 强化学习的数学原理-Notes 1
categories: [Artificial Intelligence]
tags: [Reinforcement Learning, Mathematics]
---

## Basic concept
- Part 1: State, Action, Policy
- Part 2: Reward, Return, MDP

### Background - A grid-world example

**Action set**:
- $a_1$: up
- $a_2$: right
- $a_3$: down
- $a_4$: left
- $a_5$: unchage

### State
- *State*: agent's status with respect to the environment.
- *State space*: a set of `all` the status.
- *State Space* denoted as $S = \{s_i\}, i = 0,1,...$

### Action
- *Action*: make agent from current status to next status.
- *Action Space*: a set of all actions.
- *Action Space* denoted as $A = {a_i}, i=0,1,...$
- **Different states have different action space.**
- In general, $A(s_i) = A = {a_1,a_2,...}$ for all $i$.
- Maybe change status, maybe not.

### State transition
- *State transition*: the process of agent from one state to another.
- $s_i \stackrel{a}\longrightarrow s_{i+1}$

### Policy
the action that agent choose

### Reward
the feedback about each action
- Reward: a real number

### Returns
return = sum of rewards of a policy

### Trajectories & episodes


### MDP (Markov Decision Process)

Markov Process: MDP with determined policy 
Markov Decision Process: