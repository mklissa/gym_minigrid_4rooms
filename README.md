# Classic Four Rooms implemented within the Minimalistic Gridworld Environment (MiniGrid)



Requirements:
- Python 3.5+
- OpenAI Gym
- NumPy
- Matplotlib (optional, only needed for display)

# Why this repo?

It is an implementation of the classical FourRooms environemnt from the original options [paper](https://www.cs.mcgill.ca/~dprecup/publications/SPS-aij.pdf). However, here we do not assume that the features are tabular, but rather an image that can be passed through a neural network.

# Why modify MiniGrid's repo?

We want the agent to be able to move up, down, left and right. However, in the MiniGrid's repo the agent can turn while remaining in the same location. We want to avoid that as to be able to print insightful plots such as

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


