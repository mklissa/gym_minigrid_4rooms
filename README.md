# Classic Four Rooms implemented within the Minimalistic Gridworld Environment (MiniGrid)

[![Build Status](https://travis-ci.org/maximecb/gym-minigrid.svg?branch=master)](https://travis-ci.org/maximecb/gym-minigrid)

There are other gridworld Gym environments out there, but this one is
designed to be particularly simple, lightweight and fast. The code has very few
dependencies, making it less likely to break or fail to install. It loads no
external sprites/textures, and it can run at up to 5000 FPS on a Core i7
laptop, which means you can run your experiments faster. A known-working RL
implementation can be found [in this repository](https://github.com/lcswillems/torch-rl).

Requirements:
- Python 3.5+
- OpenAI Gym
- NumPy
- Matplotlib (optional, only needed for display)

# Why this repo?

It is an implementation of the classical FourRooms environemnt from the original options [paper](https://www.cs.mcgill.ca/~dprecup/publications/SPS-aij.pdf). However, here we do not assume that the features are tabular, but rather an image that can be passed through a neural network.

# Why modify MiniGrid's repo?

We want the agent to be able to move up, down, left and right. However, in the MiniGrid's repo the agent can turn while satying in the same location. We want to avoid that as we want to be able to print insightful plots such as

<p align="center">
<img src="/figures/four-rooms-visuals.png" width=380>
</p>

where a state-dependent function is evaluated and plotteed for each location. This is very useful for debugging.

# How to use?

```
import gym
import gym_minigrid

class Minigrid2Image(gym.ObservationWrapper):
    def __init__(self, env):
        gym.ObservationWrapper.__init__(self, env)
        self.observation_space = env.observation_space.spaces['image']

    def observation(self, observation):
        return observation['image']

from gym_minigrid import wrappers as wrappers
env = wrappers.FullyObsWrapper(gym.make('MiniGrid-FourRooms-v0', max_steps=100))
env = Minigrid2Image(env)
```


