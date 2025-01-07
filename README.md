---
title: "RL-GPT: Integrating Reinforcement Learning and Code-as-policy (NeurIPS 2024) Blog"
author: "Kazi Reyazul Hasan (1905082), Mubasshira Musarrat (1905088), Arko Sikder (1905109)"
date: "2025-01-07"
---

# RL-GPT: A Smarter Way to Teach AIs Through Planning and Practice

When it comes to building intelligent systems, there’s often a tension between **explicit, rule-based coding** and **reinforcement learning** (RL). Rule-based coding is fast for simple tasks but lacks adaptability. RL excels at adapting to complex tasks, but it can be slow or data-hungry. **RL-GPT** aims to combine both worlds by merging **Large Language Models (LLMs)** with **Reinforcement Learning** for an AI that is both strategic and adaptable. This blog will introduce you to RL-GPT, explain how it works, and highlight why it’s a significant step forward.


- **Goal:** Enhance AI’s skill in solving complex, real-world tasks.
- **Problem:** LLMs know a lot but lack the ability to practice and adapt to dynamic tasks in real-world scenarios.
- **Proposed Solution:** Integrate LLMs with Reinforcement Learning (RL), creating a hybrid system for strategic planning and adaptive learning.

---

## Table of Contents
1. [What is RL-GPT?](#what-is-rl-gpt)
2. [Why Combine LLMs and RL?](#why-combine-llms-and-rl)
3. [Two-Agent Architecture](#two-agent-architecture)
4. [Key Components and Benefits](#key-components-and-benefits)
5. [Example Use Case: Minecraft Tree Chopping](#example-use-case-minecraft-tree-chopping)
6. [Going Deeper: Finding Diamonds in Minecraft](#going-deeper-finding-diamonds-in-minecraft)
7. [Technical Deep Dive](#technical-deep-dive)
8. [Demonstration of Results](#demonstration-of-results)
9. [Why This Matters Beyond Minecraft](#why-this-matters-beyond-minecraft)
10. [Deeper Insights: Strengths and Limitations of RL-GPT](#deeper-insights-strengths-and-limitations-of-rl-gpt)
11. [Wrapping Up](#wrapping-up)
12. [References](#references)

---

## What is RL-GPT?

**RL-GPT** is an AI framework that combines:
- **Large Language Models (LLMs)** like GPT-4, which excel at reasoning and breaking down tasks.
- **Reinforcement Learning (RL),** which teaches AI to learn from trial and error.

The goal is to make AI systems that can both **plan** complex actions (using LLMs) and **adapt** through real-world practice (using RL).

---

## Why Combine LLMs and RL?

1. **LLMs:** 
   - Good at splitting tasks into smaller steps.
   - Can generate structured explanations and code (“Code-as-Policy”).

2. **RL:** 
   - Masters complex tasks through repeated practice.
   - Improves adaptability when faced with new challenges.

By **blending these two** strengths, RL-GPT can handle tasks that are too intricate for simple coding but too large or dynamic for naive RL alone.

---

## Two-Agent Architecture

RL-GPT is designed around two complementary agents:

### 1. The Slow Agent (Planner)

- **Role:** Develop a strategic plan.
- **Example:** If the task is to build a house in Minecraft, the Slow Agent decides to:
  1. Collect wood.
  2. Craft planks.
  3. Build walls and a roof.
- **Technology:** Often a GPT-4 class model for high-level reasoning. It **writes** or **adapts** code, decides when RL is needed, and defines reward functions.

### 2. The Fast Agent (Doer)

- **Role:** Execute tasks in real time.
- **Method:** Uses a mix of **code** (for straightforward tasks) and **RL** (for tasks that benefit from practice and adaptation).
- **Example:** Chopping a tree in Minecraft might involve coded instructions to “attack” the trunk repeatedly, while navigating to a tree might require RL if the environment is complex.

---

## Key Components and Benefits

1. **Task Decomposition**  
   LLMs break large tasks into smaller subtasks. This makes it easier for the RL agent to learn or for code to be written directly.

2. **Adaptive Learning**  
   RL handles the unpredictable parts of the environment. No need to script every single possibility.

3. **Efficiency**  
   - *Code-as-Policy:* Fast execution for repetitive tasks.  
   - *RL:* Used selectively for parts requiring adaptation.

4. **Knowledge Transfer**  
   The LLM’s extensive training can guide the RL agent, providing domain knowledge like “diamonds are usually found at lower underground levels in minecraft.” We are coming back to this example shortly.

---

## The Critic Agent and the Two-Loop Process

While the **Slow Agent** and **Fast Agent** form the core of RL-GPT, the system also includes a **Critic Agent** that provides critical feedback on each sub-action. This architecture employs a **two-loop** iterative mechanism to continuously refine both planning and execution:

![RL-GPT Architecture: The Slow Agent, Fast Agent, and Critic Agent operating in two loops.](https://i.postimg.cc/PrLQ0zDk/rl-gpt-1.png)

1. **Inner Loop (Fast Agent + Critic Agent + Environment)**  
   - The **Fast Agent** executes sub-actions (either via generated code or learned RL policies).  
   - The **Critic Agent** observes the environment before and after each action to provide immediate feedback or critique.  
   - This feedback helps the Fast Agent adjust its behavior in real time (e.g., whether it’s moving closer to a goal or wasting resources).

2. **Outer Loop (Slow Agent + Fast Agent)**  
   - The **Slow Agent** interprets the Critic Agent’s feedback, updating its overall strategy or decomposing tasks differently if needed.  
   - It may generate new code snippets, refine the RL configuration, or restructure sub-actions.  
   - The **Fast Agent** then implements these changes in the next iteration of the inner loop.


## Example Use Case: Minecraft Tree Chopping

### High-Level Plan (Slow Agent)
1. Identify the nearest tree.
2. Move toward the tree.
3. Chop it down.

### Execution (Fast Agent)

- **Identifying the Tree**  
  Uses RL to handle uncertain environments—detect if an obstacle is in the way, figure out which direction to move, etc.

- **Chopping the Tree**  
  A piece of Python code runs a loop to repeatedly “attack” the tree:

```python
# Chop the tree 20 times
for _ in range(20):
    action[5] = 3  # "attack" action
    yield action
```

## Going Deeper: Finding Diamonds in Minecraft

Diamond mining in Minecraft is much more challenging than chopping a single tree. It requires **resource gathering**, **underground exploration**, and **hazard avoidance**. Let’s look at how RL-GPT handles this more complex scenario.

---

### Overall Strategy

1. **Gather Basic Resources**  
   - **Wood** for crafting tools.  
   - **Stone & Iron** for stronger pickaxes.  
   - **Torches** to light up caves.

2. **Craft Essential Items**  
   - **Pickaxes:** Iron pickaxes to break diamond ore.  
   - **Armor:** Survive hostile mobs (zombies, skeletons).

3. **Explore the Underground**  
   - **Navigation:** Move through randomly generated cave networks.  
   - **Hazard Avoidance:** Avoid lava pools and mobs.

4. **Extract Diamonds**  
   - **Mining:** Carefully break diamond ore blocks.  
   - **Inventory Management:** Store diamonds safely.

---

### Slow Agent (Strategic Planning)

The **Slow Agent** (a GPT-4 model) plans a logical sequence of sub-tasks:

1. **Break Down the Objective:**  
   - Identify *which sub-tasks can be coded* (e.g., crafting recipes).  
   - Determine *which sub-tasks need RL* (e.g., cave navigation).

2. **Define Rewards:**  
   - Provide *dense rewards* for partial progress, like mining iron or reaching certain depths.

3. **Generate Code:**  
   - Output Python scripts for repetitive tasks like crafting or placing torches.

4. **Update the Plan as Needed:**  
   - Monitors feedback from the Fast Agent to adjust strategies if progress stalls.

> **Example Planning Prompt (Slow Agent)**  
> 1. Craft iron pickaxe.  
> 2. Collect torches.  
> 3. Move to **y-level 12** underground.  
> 4. Avoid lava blocks.  
> 5. Mine diamond ore if detected.

---

### Fast Agent (Execution)

The **Fast Agent** actually *does* the work:

1. **Code Execution**  
   - Implements the Slow Agent’s Python scripts for tasks like crafting items.  
   - Handles straightforward actions (e.g., “Place a torch every 10 blocks”).

2. **Reinforcement Learning**  
   - Learns *how* to navigate dark caves, avoid mobs, and find diamonds.  
   - Uses reward signals that encourage it to *reach lower y-levels*, *pick up diamonds*, and *stay alive*.

3. **Interaction Loop**  
   - Reports back successes, failures, or unexpected events to the Slow Agent.  
   - Receives updated code or new reward functions if needed.

---

### Key Challenges in Diamond Mining

| **Challenge**           | **How RL-GPT Addresses It**                                     |
|-------------------------|-----------------------------------------------------------------|
| **Resource Gathering**  | Coded sub-tasks (crafting, collecting wood, smelting iron)      |
| **Underground Navigation** | RL-based pathfinding (reward for reaching deeper levels safely) |
| **Mobs and Hazards**    | RL to learn avoidance or combat strategies                      |
| **Sparse Rewards**      | Carefully shaped rewards (e.g., small points for progress, big points for diamond) |

---

## Technical Deep Dive

### 1. Reward Function in RL

**Example Reward Function**:  
```math
R_{\text{diamond}} = \frac{1}{T} \sum_{t=1}^{T}
\Bigl(
   \alpha \cdot \text{progress\_toward\_diamond}(t)
   \;-\;
   \beta \cdot \text{damage\_taken}(t)
   \;-\;
   \gamma \cdot \text{time\_cost}(t)
\Bigr),
```
where

- **T** is the total number of timesteps (or episodes).
- **α** is a positive weight rewarding progress toward diamond ore.
- **β** penalizes the agent for any health lost (e.g., from mobs or lava).
- **γ** penalizes excessive time spent or idle actions.

Each term `progress_toward_diamond(t)` measures how much closer the agent is to obtaining a diamond at timestep `t`.  
The function `damage_taken(t)` tracks how much health was lost,  
and `time_cost(t)` optionally penalizes the agent for slower execution or unnecessary wandering.
> The reward function is generated using gpt-4 for obvious reasons 😊.

### 2. Code-as-Policy: Crafting and Inventory Management

**Coding** certain tasks accelerates learning:

```python
def craft_item(item_name, quantity):
    """
    Craft a specified number of items, assuming 
    needed resources are in inventory.
    """
    for _ in range(quantity):
        action = create_crafting_action(item_name)
        yield action
```

The **Slow Agent** generates such code to handle straightforward tasks—like crafting items or managing inventory **without** requiring trial-and-error. By contrast, the **Fast Agent** executes these scripts directly, which saves time and computational resources.

### 3. RL for Exploration

Reinforcement Learning (RL) addresses the **dynamic aspects** of tasks like **cave exploration** in Minecraft, where the environment can be unpredictable. Concretely, the RL agent:

1. **Receives a state** (e.g., the blocks nearby, health level, inventory contents).  
2. **Chooses an action** (move forward, turn left, jump, etc.).  
3. **Observes a reward** (positive for progress, negative for hazards like lava or mobs).

Over time, the policy evolves to find diamonds more reliably while minimizing dangers such as lava incidents or mob encounters.

---

## Demonstration of Results


RL-GPT excels in **long-horizon tasks** within Minecraft, as shown by two primary evaluations:

### Table 1: The ObtainDiamond Task

When tackling the more **challenging “Obtain Diamond”** task in Minecraft just discussed above, RL-GPT shows considerable advantages in both **sample efficiency** and **success rate** compared to existing methods:


| **Method**      | **Type**   | **Samples** | **Success** |
|-----------------|-----------:|------------:|-----------:|
| **DreamerV3**   | RL         | 100M        | 2%         |
| **VPT**         | IL+RL      | 16.8B       | 20%        |
| **DEPS-BC**     | IL+LLM     | --          | 0.6%       |
| **DEPS-Oracle** | LLM        | --          | 60%        |
| **Plan4MC**     | RL+LLM     | 7M          | 0%         |
| **RL-GPT**      | RL+LLM     | 3M          | **8%**     |

- Methods like **DreamerV3** require **100 million** environment steps to achieve a 2% success rate.
- **VPT** uses **16.8 billion** steps (plus expert data) to reach 20%, **DEPS-Oracle** requires **hand-crafted policies** for subtasks.
- **RL-GPT**, by contrast, achieves **8%** success with only **3 million** steps—demonstrating strong **sample efficiency** and the benefit of combining RL with GPT-based planning.

### Table 2: Comparison on MineDojo Tasks

Below is **Table 2** from the study, comparing several tasks selected from the **MineDojo benchmark**. RL-GPT achieves the highest success rate on all these tasks (e.g., obtaining a stick, crafting a table, etc.):


| **Task**                  | **MineAgent** | **MineAgent (AutoCraft)** | **Plan4MC** | **RL-GPT** |
|--------------------------:|--------------:|--------------------------:|------------:|-----------:|
| **Stick**                 | 0.00          | 0.00                      | 0.30        | **0.65**   |
| **Crafting Table**        | 0.00          | 0.03                      | 0.30        | **0.65**   |
| **Wooden Pickaxe**        | 0.00          | 0.00                      | 0.53        | **0.67**   |
| **Stone**                 | 0.00          | 0.00                      | 0.37        | **0.67**   |
| **Stone Pickaxe**         | 0.00          | 0.00                      | 0.17        | **0.64**   |
| **Bucket**                | --            | 0.46                      | 0.83        | **0.85**   |
| **Furnace**               | --            | 0.50                      | 0.53        | **0.56**   |
| **Raw Beef (Steak)**      | --            | 0.33                      | 0.43        | **0.46**   |
| **Cooked Steak**          | --            | 0.35                      | 0.33        | **0.38**   |
| **Bed**                   | --            | 0.00                      | 0.17        | **0.32**   |

- **Key Observation**: RL-GPT consistently outperforms both **MineAgent** (with and without AutoCraft) and **Plan4MC** across a variety of sub-goals.

### Visualization: Iterative Tree Harvesting

Below is a **visual demonstration** of how RL-GPT learns to **harvest a tree log** over multiple iterations, compared to other baselines. Each row shows an agent’s attempts at cutting down a tree; the captions describe how **RL-GPT** progressively refines its approach by combining **code generation** (to handle simpler subtasks) with **RL** (to address dynamic decisions).

![Figure: Demonstrations of how different agents learn to harvest a log. RL-GPT splits the task into “find a tree” (code) and “cut a log” (RL). After refining in several iterations, it achieves a 58% success rate.](https://i.postimg.cc/DZn8PFrz/rl-gpt2.png)

> **Key Observations:**
>
> - **Pure RL or Pure Code** solutions often get stuck or fail to generalize.  
> - **RL-GPT** decomposes the task into smaller subtasks (e.g., *find a tree*, *aim at the trunk*, *attack 20 times*) and solves them incrementally.  
> - **Success Rate** climbs from 0% in the initial iteration (iter-0) to **58%** by iter-3, showcasing the power of **iterative refinement**.  

---



## Why This Matters Beyond Minecraft

1. **Robotics**  
   - RL-GPT could plan high-level tasks like “navigate to a storage room,” while the RL component handles **real-world uncertainties** such as obstacles or sensor noise.

2. **Customer Support**  
   - Basic data retrieval scripts can be generated by the Slow Agent, leaving the Fast Agent’s RL capability to handle **complex user interactions** or unique customer requests.

3. **Automation**  
   - Complex pipelines, for instance in **shipping logistics** can blend **coded rules** with **RL-driven** scheduling and routing to adapt dynamically as demands shift.

---

## Deeper Insights: Strengths and Limitations of RL-GPT

While **RL-GPT** demonstrates remarkable progress in decomposing and solving complex tasks, it’s important to understand both its strengths and the challenges it faces:

### Strengths
1. **Flexible Task Decomposition**  
   RL-GPT uses GPT-style language models to break down tasks into smaller subtasks. This modularity helps streamline learning by focusing RL only where it's actually needed.
2. **Sample Efficiency**  
   By taking off repetitive or deterministic actions to code (Code-as-Policy), RL-GPT reduces the burden on reinforcement learning, lowering the total number of environment interactions needed.
3. **Iterative Refinement**  
   The dual-loop feedback mechanism where the Slow Agent refines its plan based on feedback from the Critic Agent produces rapid incremental improvements, especially on long-horizon goals.
4. **Generalizable Architecture**  
   Although showcased in Minecraft, RL-GPT can be adapted to robotics, logistics, and other domains where tasks can be partially scripted and partially learned.

### Limitations
1. **Reliance on Accurate Task Decomposition**  
   If the Slow Agent’s breakdown of subtasks is flawed or too coarse, the Fast Agent may struggle to learn effective policies.
2. **Complexity of Real-World Deployment**  
   While RL-GPT proves effective in simulated environments, real-world scenarios (e.g., robotics) introduce noisy sensors, hardware constraints, and safety concerns that may complicate the planning-execution loop.
3. **Long Fine-Tuning Cycles**  
   Iterative refinement can be time-consuming for very large or complex tasks, especially when environment resets or multi-stage training are required.
4. **Limited Autonomy in Novel Tasks**  
   RL-GPT still requires some **human priors** or high-level guidance to jumpstart subtasks. Completely autonomous decomposition and reward design for unfamiliar domains remain active research areas.

Overall, RL-GPT’s **two-agent plus Critic Agent** model showcases how merging language-based planning, code-driven policies, and reinforcement learning can yield sample-efficient solutions. However, deploying this approach in more varied or unpredictable real-world settings will require further advances in task decomposition, reward shaping, and environmental interactions.

---

## Wrapping Up

**RL-GPT’s two-agent architecture** (Slow Agent for planning, Fast Agent for execution) provides a **balanced** approach to tackling complex tasks. By utilizing:

- **LLMs** for strategic planning and code generation, and
- **Reinforcement Learning** for adaptive, real-time decision making,

this framework achieves **greater efficiency** and **improved adaptability**. While Minecraft is a convenient testing ground, RL-GPT’s principles can be applied to **real-world tasks** from manufacturing to multi-step workflows, where a combination of **predefined logic** and **adaptive learning** can shine.

---

## References

- **RL-GPT Research Paper**: [OpenReview](https://openreview.net/pdf?id=LEzx6QRkRH)  




