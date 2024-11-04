# Isaac Gym (Depcrecated)
Isaac Gym is NVIDIA's prototype physics simulation environment for reinforcement learning research. Isaac Gym allows developers to experiment with end-to-end GPU accelerated RL for physical systems. Unlike other similar RL gyms, Isaac Gym can run simulations on the GPU and store results in GPU tensors rather than copying them back to CPU and memory. Also provides a Tensor-backed API to access these results, allowing RL observations and rewards calculations to also take place on GPU.

Isaac Gym also include a basic PPO implementation and a simple RL task system that can be used with it. Users may substitute alternative task systems and RL algorithms as desired.


## Installation via Conda

### Pre-requisites:
- Pyenv with Python 3.8
- Ubuntu 20.04


### Setting up Isaac Gym:
1. Install Pyenv using the instructions provided [here](https://www.dedicatedcore.com/blog/install-pyenv-ubuntu/)
2. Install Miniconda by following the instructions [here](https://docs.anaconda.com/miniconda/). Don't forget to add miniconda to path, run `conda init` and `conda config --set auto_activate_base false`
3. Down the Isaac Gym repository from [here](https://developer.nvidia.com/isaac-gym)
4. Move the `isaacgym` folder to `$PROJECT_HOME/isaacgym`
5. Modify the `isaacgym/python/setup.py` to have the following versions of libraries,
```
"torch=1.8.1",
"torchvision=0.9.1",
"numpy=1.16.4",
"scipy=1.5.0",
"pyyaml=5.3.1",
"pillow",
"imageio",
"ninja",
```
6. Switch to `isaacgym` and run `./create_conda_env_rlgpu.sh` to create the conda environment and wait...this can take 15-30 mins depending on your internet speed.
7. You now have a conda env named `rlgpu` with all the dependencies installed. Run `conda activate rlgpu` to activate this environment.
8. NOTE: For interacting with Isaac Gym, it is necessary to have `rlgpu` environment activated.
8. To test the Isaac Gym installation, run `cd isaacgym/python/examples && python joint_monkey.py` to watch a demo of a trained agent flexing all its joints.


### Setting Go2 in Isaac Gym: (WIP)
TBA