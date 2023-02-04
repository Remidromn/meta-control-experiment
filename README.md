# Meta-control decision-making experiment

## Overview 

This program has been developed during my thesis: ["Dromnelle, R. (2021). Architecture cognitive générique pour la coordination de stratégies d'apprentissage en robotique (Doctoral dissertation, Sorbonne université)."](https://www.theses.fr/2021SORUS039) It allows an agent to solve learning problems in abstract virtual environments containing reward.

The main objective of my thesis was to create a meta-control algorithm that allows an agent to coordinate several online behavior strategies based on reinforcement learning. This program allowed me to quickly evaluate several coordination criteria in simulation before performing experiments in the real environment with a real robot. 

## Script to simulate an agent evolving / acting in an environment containing a reward source

* The *agentSimulator.py* script is the core of the program.

  It takes as input 7 mandatory ordered arguments :
  1.  the id of the experiment that we are going to launch. It must be an integer.
  2.  the id of the first expert, among this list : MF, MB, DQN, None.
  3.  the id of the second expert among this list : MF, MB, DQN, None.
  4.  the file that contains the representation of the environment,
  5.  the file that describes the key states of the environment,
  7.  the file that describes the state space and the action space,
  7.  the file that contains the parameters of the agent.
  
  In addition, it can also take 9 optional arguments :
  * (-c) the coordination criterion the agent will use, among this list : random (default value, entropy, entropy_and_cost, only_one.
  * (-k) the value of the kappa coefficient (-k),
  * (-r) the amount of reward expected before the simulation stops (-r),
  * (-d) the maximum duration of the simulation (-d),
  * (-w) the window size of the filtering (-w),
  * (-n) the indication of an upcoming goal change for the agent (-n),
  * (-a) the indication of an upcoming environmental change (-a),
  * (-l) the record of the data (-l),
  * (-s) the record of a compressed version of the data (-s).
  
* The *modelFreeRL.py* script allows the agent to use a Q-learning algorithm (model-free reinforcement learning) 
to learn to solve the task,
* The *modelBasedRL.py* script allows the agent to use a Value-Iteration algorithm (model-based reinforcement learning) to learn to solve the task,
* The *DQN.py* script allows the agent to use a Deep Q-Network algorithm (deep reinforcement learning) 
to learn to solve the task,
* The *prioritizedSweeping.py* script allows the agent to use a Prioritized Sweeping algorithm (model-based
reinforcement learning) to learn to solve the task,
* The *metaControllerSystem.py* script allows the agent to coordinate the different behavioral strategies implemented in the four previous scripts,
* The *manageEnvironment.py* script allows to set up the environment and simulate the actions of the agent on it,
* The *utility.py* script contains some functions used by the other scripts.

 ## Files that describe the navigation environment presented in my thesis
 
 * The *realisticNavWorld.jso* file is a transition model generated by a Turtlebot having explored a navigation arena for 13 hours. This transition model contains the consequences of each action of the agent in the environment, in the form of a set of discrete probabilities. We can see it as an "image" of the real environment, where only the information of interest is kept, that is to say in this case only what happens when the agent moves in such direction. 
* The *realisticNavWorld_wall20-21.json* file is identical to the realisticNavWorld.json file, with the addition of a wall between the states 20 and 21,
* The *realisticNavWorld_wall6-7.json* file is identical to the realisticNavWorld.json file, with the addition of a wall between the states 6 and 7,
* The *realisticNavWorld_afterSwitch.json* file is identical to the realisticNavWorld.json file, with a change in the location of the reward, from the state 18 to the state 34,
* The *keyStates.txt* file contains the id of the rewarded states and the initial states,
* The *spaces.txt* file contains the actions space and the states space,
* The *parameters.txt* file contains the parameters of the agent.
 
## Dependencies

* python 3
* numpy
* tensorflow

## Example of a command to run the program

python agentSimulator.py 0 MF MB realisticNavWorld.json keyStates.txt spaces.txt parameters.txt -d 1600 -c entropy_and_cost

