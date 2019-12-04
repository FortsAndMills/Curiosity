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
* **Flow-based ICM** [Exploration via Flow-based Intrinsic Rewards](https://openreview.net/pdf?id=SkxzSgStPS)
  + suggests paying attention to the motion in the picture (is it always relevant?). Comparable to ICM.
* **Random Network Distillation** [Exploration by Random Network Distillation](https://arxiv.org/pdf/1810.12894.pdf)
  + solves Montezuma's Revenge!
  - is not reproduced on Mario (see plots in previous paper...)
  
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

**22/09/19.** [See MountainCar.ipynb](https://github.com/FortsAndMills/Curiosity/blob/master/%5BLRL%5D%20MountainCar.ipynb)

Basic version of curiosity is added to [LRL library](https://github.com/FortsAndMills/Learning-Reinforcement-Learning/tree/master/LRL). Just inverse model, trying to predict *a* based on *s* and *s'*. Loss of this inverse model is considered as intrinsic motivation (self-supervised reward) and summed with extrinsic reward. First experiment is on MountainCar (perfect simple environment!)
  
  (+) it worked
  
  (+) although I took hyperparameters from thin air
  
  (-) was not really stable
  
  (-) inverse model by some reason required thousands of iterations to converge, although classification task is really simple (4 features to 3 classes with easy dependency)
  
  **01/10/19.** Failed to install Sonic; failed to install Mario. No games - no pain - no gain.
  
  **07/10/19.** Mario is installed! Hurey! Some hands on, still with just inverse model...
  
  **27/10/19.** [See Mario.ipynb](https://github.com/FortsAndMills/Curiosity/blob/master/%5BLRL%5D%20Mario%20PPO.ipynb)
  
  Baseline results with PPO on Mario and playing with parameters. It quickly learns to go to the right, but still fails to stably jump over enemies. After 60 hours of training, average reward stops growing, but Mario still can touch enemies, misses a lot of bonuses and has problems with jumping over first pitfall. The second one is even larger and is his current doom.
  
  There is some strange preprocessing of environment where Mario is almost lost on the screen, but it is taken from original article. Also, experiments with network working with large-scale image did not lead to better results either. Inverse model has serious problems with learning, while DQN also has some issues. Nevertheless, there are some articles about DQN on Mario...
  
  ![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_ppo_rewards.png) ![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_ppo.gif)
  
  **10/11/19** Refactoring is coming to its end. We are finally moving to [Lego Reinforcement Learning](https://github.com/FortsAndMills/Lego-Reinforcement-Learning)
  
  **26/11/19** Refactoring pt.II has finished. Rainbow DQN and Actor-Critic are restored. Self-supervision/PPO/RNN in plans...
    
  **04/12/19.** [See Mario Rainbow.ipynb](https://github.com/FortsAndMills/Curiosity/blob/master/%5BLegoRL%5D%20Mario%20Rainbow.ipynb)
  
  Baseline using reward taken from [this github](https://github.com/uvipen/Super-mario-bros-A3C-pytorch); it motivates agent to move further in the level and ignore monets / enemies. This allows to set gamma=0.9. Rainbow DQN turned out to be extremely slow, so only 2000+ games during 84 hours of training. Learned to pass first level and got stuck in the tunnel on the second level.
  
![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_rainbow_cr.png) ![](https://github.com/FortsAndMills/Curiosity/blob/master/results/Mario_rainbow_cr%20(iter.%20291000).gif)
