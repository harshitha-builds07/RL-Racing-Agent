## Project Overview

This project implements an autonomous racing agent capable of learning how to navigate a simple 2D racing track using Reinforcement Learning (RL). Unlike traditional programming where every driving rule is manually defined, the agent learns through continuous interaction with the environment by receiving rewards and penalties based on its actions.

The objective of this project was to understand how different reinforcement learning design choices—such as the observation space, action space, reward function, and training configuration—influence the behaviour learned by the agent.

To analyse the learning process, two experiments were conducted. The first experiment used a simple reward function and shorter training, resulting in poor driving behaviour. Based on those observations, the reward function and training duration were improved, leading to significantly better navigation performance.

---

# Objectives

* Build a custom 2D racing environment.
* Train an autonomous racing agent using Reinforcement Learning.
* Understand how an RL agent learns through trial and error.
* Design suitable observation and action spaces.
* Study the effect of reward function design.
* Compare baseline and improved agent performance.
* Analyse failed behaviour and improve the agent.

---

# Technologies Used

* Python
* Gymnasium
* Stable-Baselines3
* PPO (Proximal Policy Optimization)
* NumPy
* Matplotlib
* Google Colab

---

# Reinforcement Learning Concepts Used

## Environment

The environment consists of a custom-built elliptical racing track where the car interacts with the surroundings. At every step, the environment updates the car's position, checks whether it remains on the track, computes rewards, and determines whether the episode should terminate.

---

## State (Observation Space)

The agent receives the following information from the environment:

* Car X position
* Car Y position
* Heading angle
* Current speed
* Front distance sensor
* Left distance sensor
* Right distance sensor

These observations allow the agent to estimate its current position and surroundings before deciding its next action.

---

## Action Space

The agent can perform one of five discrete actions:

| Action | Description   |
| ------ | ------------- |
| 0      | Turn Left     |
| 1      | Move Straight |
| 2      | Turn Right    |
| 3      | Accelerate    |
| 4      | Decelerate    |

These actions are sufficient for controlling the racing car without making the action space unnecessarily complex.

---

# Reward Function

The reward function encourages the agent to stay on the track while moving efficiently.

The improved reward function includes:

* Positive reward for staying alive.
* Additional reward proportional to distance travelled.
* Bonus reward for maintaining speed.
* Small penalty every timestep to encourage quicker completion.
* Large negative reward when the car leaves the track, terminating the episode.

This reward structure encourages smooth driving instead of remaining stationary.

---

# Training Process

The agent was trained using the PPO algorithm from Stable-Baselines3.

Training procedure:

1. Initialize the custom Gymnasium environment.
2. Start with random actions.
3. Collect observations, rewards, and transitions.
4. PPO updates the policy network after each rollout.
5. Repeat training over multiple episodes.
6. Gradually improve the driving policy through trial and error.

---

# Experiment 1 – Baseline Reward Design

The first experiment used a simple reward structure and shorter training.

### Observations

* The agent mostly learned to drive straight.
* Steering behaviour was very limited.
* The car terminated the episode before completing meaningful laps.
* Learning was unstable because the reward function did not sufficiently encourage balanced driving behaviour.

This experiment demonstrated that simply rewarding survival is not enough for learning efficient navigation.

---

# Experiment 2 – Improved Reward Design

Based on the limitations observed in Experiment 1, several improvements were introduced.

### Improvements

* Added movement-based reward.
* Added speed reward.
* Added small timestep penalty.
* Increased total training timesteps.
* Tuned the reward balance for smoother learning.

### Results

The trained agent showed noticeable improvement:

* Stayed on the track for much longer.
* Successfully navigated multiple turns.
* Produced smoother trajectories.
* Achieved higher cumulative rewards.
* Learned a more stable driving policy compared to the baseline experiment.

---

# Failed Behaviour

One important failed behaviour observed during development was that the baseline agent frequently drove almost straight without learning effective steering behaviour. Since the reward function mainly encouraged survival, the agent failed to understand that controlled turning was necessary for completing the racing track.

This highlighted how strongly the reward function influences the policy learned by a reinforcement learning agent.

---

# Why PPO?

PPO (Proximal Policy Optimization) was selected because:

* It provides stable policy updates.
* It is easy to implement using Stable-Baselines3.
* It performs well for continuous interaction tasks.
* It requires minimal hyperparameter tuning compared to many other RL algorithms.
* It is widely used for robotics and autonomous navigation problems.

---

# Design Decisions

## Why Gymnasium?

Gymnasium provides a standard interface for reinforcement learning environments and integrates directly with Stable-Baselines3.

---

## Why Stable-Baselines3?

Instead of implementing PPO completely from scratch, Stable-Baselines3 was used because it provides reliable and well-tested implementations, allowing more focus on understanding environment design and reward engineering.

---

## Why Discrete Actions?

A discrete action space keeps the learning problem simpler and easier to analyse while still allowing effective vehicle control.

---

## Why not DQN?

Although DQN also supports discrete actions, PPO generally provides more stable training for sequential control tasks and is less sensitive to sudden policy updates.

---

# Conclusion

This project demonstrates how an autonomous racing agent can learn to navigate a custom racing environment using Reinforcement Learning. Through two different experiments, it became clear that the design of the reward function plays a critical role in determining the behaviour learned by the agent.

The improved reward function and longer training enabled the agent to drive more smoothly, remain on the track longer, and achieve significantly better performance than the initial baseline model. More importantly, the project provided practical understanding of state representation, action selection, reward engineering, and policy optimisation in reinforcement learning.
