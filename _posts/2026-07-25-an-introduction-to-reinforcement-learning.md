---
title: "An Introduction to Reinforcement Learning"
date: 2026-07-25
permalink: /posts/2026/07/an-introduction-to-reinforcement-learning/
---

You’re heading to work in Nairobi. The main road is usually faster early in the morning, but once traffic builds up, a side road can save you time. At the next junction, you face another choice. You could stay on the side road or rejoin the main road before a stretch that usually clears. Each turn changes which options you’ll have a few minutes later.

That’s the kind of problem **reinforcement learning** tackles. An **agent** makes decisions in an **environment** and gets feedback in the form of **rewards**. The goal is to find a strategy that earns as much reward as possible over time. In a commute example, we could give the agent a reward of minus one for every minute spent travelling. Maximising the total reward would then mean finding a strategy that gets you to work in the fewest minutes on average.

## From individual turns to a policy

At each junction, the agent observes its **state**. That could include where it is, what time it is, and how heavy traffic looks. It then chooses an **action**, such as turning left or continuing straight. The environment determines where it ends up and how long the move takes. In reinforcement learning, one complete trip from departure to arrival is an **episode**.

A turn can look good on its own and still make the whole trip worse. A clear side road might get you to the next junction in one minute, then leave you waiting ten minutes to merge. A slower first turn might put you on a road that keeps moving. The agent cares about the **return**, the rewards accumulated across the trip. That gives it a way to judge an early turn by what happens several decisions later.

The agent’s strategy is called a **policy**. A policy could say to take the main road before 7 a.m. and use the side road when traffic at the first junction is heavy. A more flexible policy might give several turns a chance of being picked. To compare those turns, the agent can estimate an **action value**, also called a **Q-value**. This estimates the return from taking a particular action in the current state and following a policy from there. The same turn can have a high value at 6:30 and a low value at 8:00.

## Model-based reinforcement learning

A **model** predicts what happens after an action. In the commute example, it might predict which junction a turn leads to and how long that stretch of road is likely to take under current conditions. Given those predictions, the agent can plan ahead. It can weigh the short, clear stretch against the chance of getting stuck at the merge.

Some parts of the model could come from a map. Others, such as how long a road takes in the rain, could be estimated from past trips. An agent that learns those travel times and then uses them to plan is doing model-based reinforcement learning.

Two classic planning methods are **value iteration** and **policy iteration**. With value iteration, the agent repeatedly revises its estimate of how good each junction is by considering the roads that leave it and where those roads lead. If it learns that one junction has a fast road to the office, that information can improve its estimates for roads that lead to that junction. With policy iteration, the agent starts with a full strategy, works out how well that strategy performs, and then changes the turns it recommends wherever a better option is available.

An accurate model can save the agent many practice trips. It can compare options using predictions before sending anyone down a road. The quality of that plan depends on the quality of the predictions. If the model still assumes a junction is open after it closes for roadworks, it can keep proposing a route that would have been fast yesterday.

## Model-free reinforcement learning

A **model-free** agent can learn from trip records directly. After enough morning trips, it might learn that turning left at a busy junction usually gets you to work sooner. It can update the value of that turn from the travel times it observes without estimating how often each downstream junction gets congested.

**Monte Carlo methods** can wait until the trip ends, then use the return from the remaining trip to update the values of turns along the way. **Temporal-difference methods**, including **SARSA** and **Q-learning**, can update after each turn. If a turn took two minutes and brought the agent to a junction it already knows well, it can combine those two minutes with its estimate of the remaining trip.

SARSA and Q-learning differ in which action they use for that estimate. SARSA uses the next action the agent actually selects. Q-learning uses the action with the highest estimated value at the next junction, even if the agent goes on to try a different turn. Both can learn from the same kind of trip records. A model-free agent may need many such trips before it can reliably tell a good turn from one that happened to work on a quiet morning.

I implemented value iteration, policy iteration, SARSA, and Q-learning in **FrozenLake**, a small grid game where an agent tries to reach a goal without falling into holes. In the slippery version, choosing a direction can send the agent to a different square than intended. That makes it a compact way to see how planning accounts for uncertain outcomes and how learning methods respond to outcomes they observe. Browse the FrozenLake notebooks for [value iteration](https://github.com/martinoywa/reinforcement-learning-notes/blob/e44f4744abb64f1251f2dcec763c87be72250d3a/tabular-rl-from-scratch/ValueIterationNotebook.ipynb), [policy iteration](https://github.com/martinoywa/reinforcement-learning-notes/blob/e44f4744abb64f1251f2dcec763c87be72250d3a/tabular-rl-from-scratch/PolicyIterationNotebook.ipynb), [SARSA](https://github.com/martinoywa/reinforcement-learning-notes/blob/e44f4744abb64f1251f2dcec763c87be72250d3a/tabular-rl-from-scratch/SARSANotebook.ipynb), and [Q-learning](https://github.com/martinoywa/reinforcement-learning-notes/blob/e44f4744abb64f1251f2dcec763c87be72250d3a/tabular-rl-from-scratch/Q-LearningNotebook.ipynb).
