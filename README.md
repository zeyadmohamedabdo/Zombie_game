# 🧟 Zombie Escape: Q-Learning Agent:

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pygame](https://img.shields.io/badge/Library-Pygame-green)
![RL](https://img.shields.io/badge/Algorithm-Q--Learning-red)
![Gymnasium](https://img.shields.io/badge/Env-Gymnasium-orange)

> A Reinforcement Learning project where an autonomous agent learns to navigate a dangerous maze, defeat zombies in a strict hierarchical order, and escape.

## 📖 Project Overview
This project implements a **Q-Learning** algorithm to solve a complex grid-world environment. Unlike standard maze solvers, this agent has a constrained objective: it must eliminate threats (Zombies) in a specific sequence based on their power levels before traversing to the exit.

**The Mission:**
1.  Navigate the 8x8 Grid.
2.  Defeat **Zombie Lvl 1** (Upper Right).
3.  Defeat **Zombie Lvl 10** (Lower Right).
4.  Defeat **Zombie Lvl 100** (Lower Left).
5.  Reach the **Exit** (Center).

## 🎥 Demo
*[<img width="1003" height="758" alt="image" src="https://github.com/user-attachments/assets/b1663813-409b-4723-be7d-aaa1c5d00f1b" />
]*
> The agent starts with zero knowledge and learns the optimal path through trial and error over 5000 episodes.

## 🧠 The RL Architecture

### 1. The Environment
* **Grid Size:** 8x8 fixed grid.
* **Obstacles:** Maze-like wall structure.
* **Entities:** Warrior (Agent), 3 Zombies (Static positions), 1 Exit.

### 2. State & Action Space
* **Action Space:** Discrete (4) -> `[UP, DOWN, LEFT, RIGHT]`
* **State Space:** The agent observes its current coordinates and the status of the zombies (Alive/Dead).

### 3. The Algorithm (Q-Learning)
The agent uses the Bellman Equation to update the Q-values:

$$Q(s, a) \leftarrow Q(s, a) + \alpha [R + \gamma \max_{a'} Q(s', a') - Q(s, a)]$$

Where:
* **$\alpha$ (Learning Rate):** How much new info overrides old info.
* **$\gamma$ (Discount Factor):** Importance of future rewards.
* **$R$:** Immediate reward received.

## 🏆 Reward System
To enforce the correct behavior, the environment utilizes a shaped reward function:

| Event | Reward/Penalty | Reason |
| :--- | :--- | :--- |
| **Reaching Exit** | **+5000** | Ultimate Goal |
| **Kill All Zombies** | **+500** | Secondary Goal |
| **Kill Lvl 100** | +2000 | High Value Target |
| **Kill Lvl 10** | +200 | Medium Value Target |
| **Kill Lvl 1** | +20 | Low Value Target |
| **Move to Target** | +5 | Heuristic to guide movement |
| **Move to Exit** | +10 | Heuristic to guide escape |
| **Hit Wall** | -1 | Penalty for collisions |
| **Wrong Order** | **-200** | **Critical Penalty** to enforce logic |

## 📂 Project Structure
```bash
├── assets/                 # Game sprites (Player, Zombies, Walls)
├── zombie_env_short.py     # Custom Gymnasium Environment logic
├── q_learning_agent.py     # The Q-Learning Class implementation
├── train_q_learning.py     # Main script to run training loop
├── q_table.npy             # Saved binary file containing the trained knowledge
├── requirements.txt        # Python dependencies
└── README.md               # Documentation


