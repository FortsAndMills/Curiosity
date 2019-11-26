## Curiosity and self-supervision in Deep Reinforcement Learning

* **Central article:** [Curiosity-driven Exploration by Self-supervised Prediction](https://pathak22.github.io/noreward-rl/resources/icml17.pdf)
  + played Mario level 1 without any reward; generalized faster to level 2
  + solved "noisy TV problem"
* **Large-scale study** [Large-Scale Study of Curiosity-Driven Learning](https://pathak22.github.io/large-scale-curiosity/resources/largeScaleCuriosity2018.pdf)
  + more details, options and computational resources
* **Unity experiment:** [Solving sparse-reward tasks with Curiosity](https://blogs.unity3d.com/ru/2018/06/26/solving-sparse-reward-tasks-with-curiosity/)
  + introduced Pyramids envrionment to challenge the approach: PPO does not work, PPO + Curiosity works
* **Google strange idea:** [Episodic Curiosity through Reachability](https://ai.googleblog.com/2018/10/curiosity-and-procrastination-in.html)
  + Google discovered there is a big huge problem in curiosity, which leads to *procrastination* ;) .
  - proposed their own curiosity model, but the idea seems a bit weird
  
**PLANNED EXPERIMENTS:**
- [x] test curiosity on Mountain Car problem
- [ ] check different variants of curiosity on Mountain car; check with different algorithms and possibly tune parameters
- [x] launch Mario environment
- [ ] reproduce curiosity on Mario
- [x] launch ML-agents
- [ ] relaunch ML-agents after system reset :{
- [ ] test (adapt?) [my RL library](https://github.com/FortsAndMills/Learning-Reinforcement-Learning) on ML-agents environments
- [ ] reproduce curiosity on Pyramids problem

**Looking around:**
- [Obstacle Tower](https://github.com/Unity-Technologies/obstacle-tower-source)
- Succesully installed [Gym Retro](https://github.com/openai/retro), but it needs ROMs of the games.

----------------------------------------------------------------------

# Experiments

**22/09/19.** [See MountainCar.ipynb](https://nbviewer.jupyter.org/github/FortsAndMills/Curiosity/blob/master/MountainCar.ipynb)

Basic version of curiosity is added to [LRL library](https://github.com/FortsAndMills/Learning-Reinforcement-Learning/tree/master/LRL). Just inverse model, trying to predict *a* based on *s* and *s'*. Loss of this inverse model is considered as intrinsic motivation (self-supervised reward) and summed with extrinsic reward. First experiment is on MountainCar (perfect simple environment!)
  
  (+) it worked
  
  (+) although I took hyperparameters from thin air
  
  (-) was not really stable
  
  (-) inverse model by some reason required thousands of iterations to converge, although classification task is really simple (4 features to 3 classes with easy dependency)
  
  **01/10/19.** Failed to install Sonic; failed to install Mario. No games - no pain - no gain.
  
  **07/10/19.** Mario is installed! Hurey! Some hands on, still with just inverse model...
  
  **27/10/09.** [See Mario.ipynb](https://github.com/FortsAndMills/Curiosity/blob/master/Mario.ipynb)
  
  Baseline results with PPO on Mario and playing with parameters. It quickly learns to go to the right, but still fails to stably jump over enemies. After 60 hours of training, average reward stops growing, but Mario still can touch enemies, misses a lot of bonuses and has problems with jumping over first pitfall. The second one is even larger and is his current doom.
  
  There is some strange preprocessing of environment where Mario is almost lost on the screen, but it is taken from original article. Also, experiments with network working with large-scale image did not lead to better results either. Inverse model has serious problems with learning, while DQN also has some issues. Nevertheless, there are some articles about DQN on Mario...
  
  ![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_ppo_rewards.png) ![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_ppo.gif)
  
  **10/11/19** Refactoring is coming to its end. We are finally moving to [Lego Reinforcement Learning](https://github.com/FortsAndMills/Lego-Reinforcement-Learning)
  
  **26/11/19** Refactoring pt.II has finished. Rainbow DQN and Actor-Critic are restored. Self-supervision/PPO/RNN in plans...
  
  ----------------------------------------------------------------
  
  ## Ideas:
    
- [ ] curiosity network can be used as world model. Let's use learned representation to fit world model. To learn in dream we then need to learn policy or Q-function from this representation, which is still logical, because why do we have two feature extractors in the system?
- [ ] test hypothesis that network predicting loss of curiosity network can be utilized as policy. Suppose we somehow want to perform the most surprising action. Second thoughts: for that we need Q-function for curiosity-only...
- [ ] why inverse model is not perfect again? We do not want big network there for effectiveness reasons, yet its loss is far from zero. May be we should subtract minimum of its loss from all reward generated by it?
