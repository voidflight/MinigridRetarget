Dependencies can be found in the requirements.txt file. If you are using an NVIDIA GPU, be sure to install the cuda toolkit, as well as the correct version of pytorch (see pytorch website for instructions).

This code is associated with this post: https://docs.google.com/document/d/1ItLPQikPk52QTjZrkE-q2fhALJi480IOPx3y_LYZeAw/edit?usp=sharing

The code can be used to train an agent using the experimental setup I described and replicate my results. To do this, run the provided file run_ppo_test.sh.

You may need to make some changes depending on your local setup. For instance, the code is currently designed to run on a single NVIDIA GPU; I think it also works with a CPU, but doesn't support other types of GPU.

By default, your results will be logged to a wandb dashboard. The graphs of interest will be labelled "key_blue_avg_return" and "key_purple_avg_return." I don't currently have streamlined code for plotting the blue key and purple key returns on the same graph; instead I download the csv's for the two graphs off of wandb, and then create a single graph using pandas and pyplot.

If you want to alter the hyperparameters, many of them are in run_ppo_test.sh - see src/ppo/utils.py for descriptions. Other important hyperparameters include (apologies for lack of organization):

- weight decay (PPOAgent class in src/ppo/agent.py)
- set of object color objectives the agent will be trained on (ppo_runner function in src/ppo/runner.py; src/environments/fetchobstacles.py)
- objective switching schedule (train_ppo function in src/ppo/train.py)

To change details about the environment (e.g. grid size, number of keys generated), register a new environment in src/environments/registration.py and change the env_id arg in run_ppo_test.sh.
