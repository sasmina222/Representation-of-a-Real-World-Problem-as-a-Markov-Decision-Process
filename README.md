# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim
To represent an Automatic Plant Watering System as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, rewards, and Python representation.

## Problem Statement

### Problem Description

An Automatic Plant Watering System decides when to water a plant based on the soil moisture level. The system identifies whether the soil is dry, moist, or wet.

If the soil is dry, the system waters the plant. If the soil is moist, the system waits. If the soil is wet, the system stops watering.

The system uses an MDP to select suitable actions, maintain proper soil moisture, and save water.


## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

For this system:

- S: Dry, Moist, Wet
- A: Water, Wait
- P: Probability of moving to the next soil condition
- R: Reward or penalty for an action
- γ: 0.9

---

## State Space

The state space represents all possible soil conditions.



```text
S = {
      Dry,
      Moist,
      Wet 
    }
```

- Dry: The soil needs water.
- Moist: The soil has sufficient moisture.
- Wet: The soil contains excess water.

---

## Sample State

Current State = Dry

The soil is dry, so the plant needs water.

A sample state is one specific example from the state space.



---

## Action Space

The action space represents all possible actions taken by the watering system


```text
A = {
     Water,
     Wait,
     Stop
}
```
- Water: Supply water to the plant.
- Wait: Wait without supplying water.
- Stop: Keep the water pump OFF.

---

## Sample Action



A sample action is one action selected from the action space.

Current State = Dry

Selected Action = Water

When the soil is dry, the system selects the Water action.

---

## Transition Probability


Transition probability describes the probability of reaching the next state after performing an action.



$$
P(s' \mid s,a)
$$


For this example, the transitions are deterministic, meaning each state-action pair has one defined next state.


| Current State | Action | Next State | Probability |
| ------------- | ------ | ---------- | ----------: |
| Dry           | Water  | Moist      |         1.0 |
| Dry           | Wait   | Dry        |         1.0 |
| Moist         | Water  | Wet        |         1.0 |
| Moist         | Wait   | Moist      |         1.0 |
| Wet           | Water  | Wet        |         1.0 |
| Wet           | Wait   | Moist      |         1.0 |



##### A probability of 1.0 means the transition always leads to the specified next state in this simplified model.
---

## Reward Function

The reward function defines the feedback received by the agent after taking an action.



$$
R(s,a,s')
$$

| Current State | Action | Next State | Reward |
| ------------- | ------ | ---------- | -----: |
| Dry           | Water  | Moist      |     +5 |
| Dry           | Wait   | Dry        |     -5 |
| Moist         | Water  | Wet        |     -2 |
| Moist         | Wait   | Moist      |    +10 |
| Wet           | Water  | Wet        |     -5 |
| Wet           | Wait   | Moist      |     +3 |

**Explanation:**

* +5: Watering dry soil is beneficial.
* -5: Leaving dry soil without water is undesirable.
* -2: Adding water to already moist soil is unnecessary.
* +10: Maintaining suitable soil moisture is rewarded.
* -5: Adding water to wet soil is undesirable.
* +3: Waiting when the soil is wet helps avoid excessive watering.

##### These rewards are illustrative values chosen for this simplified example.
---

## Graphical Representation
Draw the following simple MDP graph in your record
  
<img width="460" height="433" alt="image" src="https://github.com/user-attachments/assets/4ecdb258-d719-4ddc-9524-87de3f992297" />

The graph is a simplified illustration of the watering decisions. Write the transition probabilities from the table beside the corresponding arrows if required.



---

## Python Representation



Use Python dictionaries to represent the MDP.

```python
MDP Representation using Python
# print("Name: Sasmina S   ")
# print("Register Number:  212225230254   ")
states = {
    0: "Dry",
    1: "Moist",
    2: "Wet"
}
actions = {
    0: "Water",
    1: "Wait"
}
P = {
    0: {
        0: [(1.0, 1, 5, False)],

        1: [(1.0, 0, -5, False)]
    },
    

    1: {
        0: [(1.0, 2, -2, False)],
        
        1: [(1.0, 1, 10, False)]
    },

    
    2: {
        0: [(1.0, 2, -5, False)],
        
        1: [(1.0, 1, 3, False)]
    }
}
print("States:")
print(states)
print("\nActions:")
print(actions)
print("\nMDP Transition Table (P):")
print(P)
print("\nTransition Details:")
for state, action_list in P.items():
    for action, transitions in action_list.items():
        for probability, next_state, reward, done in transitions:
            print(
                states[state], "+", actions[action],
                "->", states[next_state],
                "| Probability:", probability,
                "| Reward:", reward
            )
```
---
## Output
<img width="444" height="278" alt="image" src="https://github.com/user-attachments/assets/1cf127a0-c138-41e7-bba7-7a76668fab1a" />

## Result
The Automatic Plant Watering System was successfully represented as a Markov Decision Process (MDP) by defining states, actions, transitions, and rewards.
The graphical representation clearly shows how watering decisions help maintain the plant's moisture level.



---

