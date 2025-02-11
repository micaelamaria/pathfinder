# PATHFINDER - USAGE EXAMPLE

A demo for the pathfinder tool using the TK (tyrosine kinase) domains of the Insulin receptor.
In this demo we are pulling the TK domains apart from each other.
The tool works in iterations, with the same stages repeating in each iteration.

1. Pulling/pushing simulations until the smallest successful force constant K is found. 
2. Equilibration with flat-bottom position restraints.
3. Repeat

## Needed files:
* pathfinder.py
* sbatch.sh (template)
* config.ini (template)

* toppar (folder) (Files for structure)
* topol.top
* step7.gro 
* index.ndx

* pull_eq.mdp (template)
* pull_TK.mdp (template)

## Setup
Here solvation, energy minimization, equilibration etc. have all been done for you.
When using this tool (except for this demo), you need to do these yourself.
* modify templates as needed and fill in config.ini
* login to mahti
* copy needed files into your mahti repo
* import gromacs and python-data (module load ...)

## Help
```
python pathfinder.py help
```
If you need help remembering which function does what, what arguments the functions take as input, or what command you ran previously, you can call the 'help' function.

## Start
```
python pathfinder.py init 0 
```
Each new iteration of simulations is started with the init command, which takes one argument as input: the number of the iteration. This will start the first round of simulations with 5 different values of K. These simulations will take about 10 hours, but if you don't want to wait, you can download the files from the folder 'XXXX', and continue to the next step.

## After init
```
python pathfinder.py contpull 0 'TK'
```
After pulling simulations, you will always continue with the contpull command, which takes 2 arguments as input: the number of the iteration and the name (abbreviation) of the domain. This command will check if any of the simulations were successful and if the best K has been found. If it has, the program will ask if you wish to continue to equilibration (yes). If it has not, it will calculate new values for K and ask if you want to run this new set of simulations (yes). In this case it should run another set of simulations. Again, these will take multiple hours. Continue with the contpull command until you continue to equilibration.
NOTE: When running contpull, if you encounter an error of type: "ValueError: the number of columns changed from 2 to 1 at row 478; use usecols to select a subset and avoid this error", ignore it for now and just run contpull again. This will be fixed.

## Continuing to equilibration
When the best force constant K has been found, the program will continue from the simulation with the best K into equilibration. This will again take multiple hours. 

## After equilibration
```
python pathfinder.py conteq 0 'TK'
```
After equilibration, the conteq command will check if the structure is equilibrated enough. The command takes two arguments as input: the number of the iteration and the name (abbreviation) of the domain. If the equilibration time was too short and the structure is not equilibrated enough, it will double the wall time and run the equilibration again. If the equilibration was successful, the program will tell you and exit, and now you are ready to continue into the next iteration if you wish. This demo however won't continue any further.
