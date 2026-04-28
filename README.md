# 🧠 Wumpus World Intelligent Agent (Python)

This project implements a complete simulation and intelligent agents for the **Wumpus World** problem, based on *Artificial Intelligence: A Modern Approach* by Russell & Norvig.

The project was developed incrementally across three assignments, evolving from a basic environment simulator to an intelligent probabilistic agent capable of reasoning under uncertainty.

---

## 📌 Project Overview

The Wumpus World is a grid-based environment where an agent must:
- Find the gold
- Avoid hazards (pits and the Wumpus)
- Escape safely with maximum reward

### 🎯 Performance Measure
- +1000 → Exit with gold  
- -1000 → Death (pit or Wumpus)  
- -1 → Each action  
- -10 → Using the arrow  

---

## 🧩 Assignment 1 — Environment & Naive Behavior

### ✅ Implemented:
- Full **Wumpus World simulator** with configurable grid size
- Random placement of:
  - Gold
  - Wumpus
  - Pits (based on probability)
- Agent actions:
  - `Forward`, `TurnLeft`, `TurnRight`, `Grab`, `Shoot`, `Climb`
- Percepts:
  - Stench, Breeze, Glitter, Bump, Scream
- Reward system handled entirely by the environment
- Simple visualization of the grid

### 🧪 Purpose:
To simulate the environment and verify correctness of the system.

---

## 🧠 Assignment 2 — Planning (Integrated)

> Note: Planning logic is integrated into the final Probabilistic Agent.

### 🚀 Features:
- State-space graph representation using **NetworkX**
- Each state includes:
  - Agent position `(x, y)`
  - Agent orientation (`north`, `south`, `east`, `west`)
- Graph edges represent actions:
  - `forward`, `turn_left`, `turn_right`

### 🛠️ Path Planning:
- Shortest path computed using **NetworkX shortest path**
- Plans optimal sequence of actions between states

### 🏁 Escape Strategy:
- When gold is found:
  1. Grab gold
  2. Plan shortest path to `(0,0)`
  3. Execute actions
  4. Climb to exit

---

## 🤖 Assignment 3 — Probabilistic Agent (ProbAgent)

### 🧠 Core Idea:
The agent uses **probabilistic reasoning** to safely explore unknown cells.

---

### 🔍 Belief State Tracking:
- Tracks:
  - Visited locations
  - Breeze locations → Pit inference
  - Stench locations → Wumpus inference
  - Whether a scream was heard (Wumpus killed)

---

### 📊 Probabilistic Modeling:
- Implemented using **Pomegranate**
- Two Bayesian Networks:
  - **Wumpus Model**: Wumpus location → Stench observations
  - **Pit Model**: Pit locations → Breeze observations

---

### ⚖️ Decision Strategy:
- Computes safety probability for each cell:
P(safe) = (1 - P(Wumpus)) × (1 - P(Pit))

- Only considers cells with:
  - **Safety ≥ 0.75**

- Selects next move based on:
  1. Highest safety probability
  2. Shortest path distance

- Falls back to returning to start if no safe options exist

---

### 🏹 Advanced Behavior:
- Uses arrow **intelligently** when a stench is detected
- Updates beliefs based on whether a scream is heard
- Avoids revisiting cells unnecessarily
- Takes **calculated risks** when required

---

## 🛠️ Technologies Used

- Python
- NetworkX (graph-based planning)
- Pomegranate (Bayesian networks for probabilistic reasoning)
- NumPy

---

## ▶️ How to Run

```bash
pip install networkx pomegranate numpy
python main.py
```
Example Environment Initialization:

```bash
env = Environment(4, 4, True, 0.2, AgentState())
agent = ProbAgent(4, 4, 0.2)
```
---

## 📊 Evaluation

The agent can be evaluated by running multiple episodes and measuring:

- Total reward
- Survival rate
- Success rate (gold retrieved and escaped)

---

## 📷 Visualization

The environment includes a simple text-based visualizer showing:

- Agent position and direction
- Pits, Wumpus, and Gold
- Grid layout evolution over time

---

## 💡 Key Learning Outcomes
- Environment simulation design
- Graph-based path planning
- State-space modeling
- Bayesian networks and probabilistic inference
- Decision-making under uncertainty

---

## 👩‍💻 Author

Ahlam Ibrahim
AI & Software Development
