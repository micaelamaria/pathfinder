# Pathfinder-project
Steered Molecular Dynamics (SMD) simulations are one of the most important tools in the rapid sampling of simple reaction coordinates. As a general rule, SMD simulations are done with ad hoc parameters for the forces that drive the simulation system from its starting state to an end state along with such reaction coordinates. As a result, the unphysiological forces are introduced into the system leading to strains and distortions that cause the sampled reaction path to deviate significantly from a more natural equilibrium path. To allay that issue, we will develop a new tool, Pathfinder, which systematically and algorithmically searches the path space by introducing the least amount of energy through external forces and performs relaxation simulations along the way. The relaxations themselves will be monitored in an automated way to check if the system has reached a state of relative equilibrium at a particular value of the reaction coordinate. Initially, the tool will be written for simpler reaction coordinates. Once the proof of concept is established we will use machine learning tools to derive a reaction coordinate from the initial SMD simulations and adapt it along the reaction path to estimate a more collective reaction coordinate dynamically. 

# Instructions
You will find the instructions in the pull_auto folder.
