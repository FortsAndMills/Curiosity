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
- [ ] launch Mario environment
- [ ] reproduce curiosity on Mario
- [x] launch ML-agents
- [ ] relaunch ML-agents after system reset :{
- [ ] test (adapt?) [my RL library](https://github.com/FortsAndMills/Learning-Reinforcement-Learning) on ML-agents environments
- [ ] reproduce curiosity on Pyramids problem
- [ ] test hypothesis that curiosity network can be used as world model
- [ ] test hypothesis that network predicting loss of curiosity network can be utilized as policy

**Looking around:**
- [Obstacle Tower](https://github.com/Unity-Technologies/obstacle-tower-source)
- [Gym Retro](https://github.com/openai/retro) finally supports Windows (may be it is time for another attempt to install it...)

----------------------------------------------------------------------

# Experiments

**22/09/19.** [See MountainCar.ipynb](https://nbviewer.jupyter.org/github/FortsAndMills/Curiosity/blob/master/MountainCar.ipynb)

Basic version of curiosity is added to [LRL library](https://github.com/FortsAndMills/Learning-Reinforcement-Learning/tree/master/LRL). Just inverse model, trying to predict *a* based on *s* and *s'*. Loss of this inverse model is considered as intrinsic motivation (self-supervised reward) and summed with extrinsic reward. First experiment is on MountainCar (perfect simple environment!)
  
  (+) it worked
  
  (+) although I took hyperparameters from thin air
  
  (-) was not really stable
  
  (-) inverse model by some reason required thousands of iterations to converge, although classification task is really simple (4 features to 3 classes with easy dependency)
