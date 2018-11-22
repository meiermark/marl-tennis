[image1]: https://github.com/meiermark/rl-control/blob/master/misc/mult_reacher_training.png?raw=true "Training"

# Reacher with 20 agents

The implemented version of the [ddpg algorithm](https://arxiv.org/pdf/1509.02971.pdf) solves the reacher environment with 20 agents after 800 episodes with a required minimum average score of 30.
After 900 the average score increases to 51. After 968 episodes the training was manually interrupted.

![Training][image1]

## Hyperparameters
number of episodes for training: 5000
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
The state is a vector with 37 variables. The action is a vector with 4 variables.
Both actor and critic use batch normalization for the states.

### Actor
Input(37) ->
Linear Layer(512) ->
RELU ->
Linear Layer(256) ->
RELU ->
Linear Layer(4)

### Critic
**Stream 1:**
Input(37) ->
Linear Layer(512) ->
RELU ->

**Stream 2:**
Input(4) ->

**Stream 1** + **Stream 2** ->
Linear Layer(256) ->
RELU ->
Dropout ->
Linear Layer(1)

## Ideas for the future:
- Replace ddpg with [PPO](https://arxiv.org/pdf/1707.06347.pdf)
- Test TRPO - Supposed to have a worse performance than PPO
- Apply the gained knowledge to the crawler environment
- Test the N-step strategy (Sutton, 1988)
