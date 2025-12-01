# Autonomous Vacuum Agent: Reinforcement Learning from Scratch 🤖🧹

An implementation of a resource-constrained autonomous agent capable of navigating a stochastic environment using **Markov Decision Processes (MDP)**. This project implements core Reinforcement Learning algorithms (**Value Iteration**, **Policy Evaluation**, and **Monte Carlo Control**) purely in Python without external RL libraries, demonstrating a first-principles understanding of AI decision-making.

---

## 📌 Project Overview

This project models an autonomous vacuum cleaner that operates within a dirty room (grid world). Unlike simple pathfinding, this agent must manage multiple resources and constraints:
- **Battery Life:** Consumed with every move.
- **Dust Storage:** Must return to base to empty when full.
- **Stochastic Movement:** The floor is slippery; there is a probability of slipping or hitting obstacles.
- **Optimality:** The agent must find the mathematical optimal policy to clean the room with the lowest cost.

## 🛠 Technical Stack
- **Language:** Python 3.x
- **Core Concepts:** Markov Decision Processes (MDP), Dynamic Programming, Monte Carlo Methods.
- **Paradigm:** Object-Oriented Programming (OOP) for state-space simulation.
- **Dependencies:** Standard Python Libraries (`itertools`, `random`). *No "Black-Box" ML frameworks used.*

---

## 🧠 Algorithms Implemented

### 1. Markov Decision Process (MDP) Modeling
The environment is modeled as a tuple $(S, A, P, R, \gamma)$:
- **States:** Grid coordinates $(x, y)$, Battery Level, Dust Level.
- **Actions:** `Up`, `Down`, `Left`, `Right`.
- **Rewards:** 
  - `+20` for cleaning a cell.
  - `-5` for hitting a wall or object.
  - `-7` for running out of battery.
  - High penalty cost for manual recharge trips.

### 2. Dynamic Programming (Model-Based)
- **Policy Evaluation:** Iteratively evaluates a fixed policy to determine the Value Function $V(s)$.
- **Value Iteration:** Computes the optimal State-Value function $V^*(s)$ by iteratively applying the **Bellman Optimality Equation**:
  $$V_{k+1}(s) = \max_a \sum_{s'} P(s'|s,a) [R(s,a,s') + \gamma V_k(s')]$$

### 3. Monte Carlo Control (Model-Free)
- Implemented **First-Visit Monte Carlo** to learn the optimal policy directly from experience (episodes).
- Uses **$\epsilon$-greedy** exploration strategy to balance exploring new paths vs. exploiting known rewards.

---

### 📊 Simulation Logic
The AutonomousVacuum class handles the physics of the world:
succReward(action): Calculates the probabilistic outcome of a move (considering hitWallProb and hitObject probabilities).
Resource Management: Logic to force the agent to return to (0,0) (Base) when Battery < 5% or Storage is full.
