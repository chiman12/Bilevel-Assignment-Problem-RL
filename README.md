## Problem Description
The problem is a bi-level hospital assignment optimization:
-Upper-level problem (patients → hospitals):
Each patient must be assigned to a hospital, considering: Travel time to the hospital, Waiting time at the hospital andHospital capacity (number of patients it can handle).

-Lower-level problem (patients → beds within hospital):
Once patients are assigned to a hospital, they must be allocated to beds, considering: Consultation time, Administrative/assignment time, Penalty if there are more patients than beds.

Objective: Minimize the total time for all patients across both levels.

The solution uses Reinforcement Learning (DQN) to dynamically assign patients to hospitals over multiple periods, accounting for growing patient populations and hospital capacities.

## Code Explication
-Lines 1–7: Install & Imports
-Lines 9–17: Lower-level objective:
Line 9: Defines lower-level objective (patients → beds).
Lines 10–12: Handles empty hospital case.
Line 13: Base time = consultation + assignment per patient.
Line 14: Adds penalty if patients > beds.
Line 15: Returns total lower-level time.
-Lines 18–30: Bilevel objective:
Line 18: Upper-level objective (patients → hospitals + lower-level).
Line 19: Converts solution to integers (hospital indices).
Lines 21–22: Adds travel + waiting time per patient.
Lines 23–25: Calls lower-level objective for each hospital.
Line 26: Returns total bilevel time.
-Lines 31–50 DQN Neural Network:
Line 31: Defines DQN network.
Lines 32–40: Initialize network: input = flattened state, hidden layer, output = Q-values per patient × hospital.
Lines 41–44: Forward pass: flatten → fully connected → reshape to (patients × hospitals).
-Lines 51–79 DQN Agent:
Lines 51–59: Initialize agent (model, optimizer, loss, hyperparameters).
Lines 60–66: select_action implements ε-greedy policy.
Lines 67–77: train updates DQN using Q-learning target.
-Lines80–104 Run RL:
Lines 80–82: Initialize state and agent.
Line 83: Compute max_possible_time for reward normalization.
Lines 84–94: RL training loop: select actions, compute normalized reward, decay epsilon, train network, update state.
Lines 95–97: Return best solution after training.
-Lines 105–116 Dynamic periods: Simulates dynamic growth of patients & hospitals across periods.
-Lines 117–125 Data generation
-Lines 126–144 Main RL loop
-Lines 145–154 Visualization
