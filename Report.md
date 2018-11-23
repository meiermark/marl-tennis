[image1]: https://github.com/meiermark/marl-tennis/blob/master/misc/training_tennis.png?raw=true "Training"

# Multi-Agent Reinforcement Learning - Tennis

The implemented version of the [ddpg algorithm](https://arxiv.org/pdf/1509.02971.pdf) solves the tennis environment after 100 episodes with a required minimum score of 0.5. The training is not very stable and worsens after 100 episodes.

![Training][image1]

## Hyperparameters
number of episodes for training: 200
max number of actions per episode: 2000
discount factor for rewards: 0.99
soft update of target parameters: 1e-3
update frequency of the networks: every 20 steps
number of updates with different samples from the memory: 10
learning rate of the actor: 1e-4
learning rate of the critic: 4e-4
weight decay for the optimizer of the critic: 0
dropout probability in the critic network: 0.2

## Networks
The state is a vector with 8 variables. The action is a vector with 2 variables.
Both actor and critic use batch normalization for the states.

### Actor
Input(8) ->
Linear Layer(512) ->
RELU ->
Linear Layer(256) ->
RELU ->
Linear Layer(2)

### Critic
**Stream 1:**
Input(8) ->
Linear Layer(512) ->
RELU ->

**Stream 2:**
Input(2) ->

**Stream 1** + **Stream 2** ->
Linear Layer(256) ->
RELU ->
Dropout ->
Linear Layer(1)

## Ideas for the future:
- The task seems to be quite symmetric, this could be exploited
