# Isaac Gym
(now deprecated 😞 but can use to recreate and run existing community work)

Isaac Gym is NVIDIA's prototype physics simulation environment for reinforcement learning research. Isaac Gym allows developers to experiment with end-to-end GPU accelerated RL for physical systems. Unlike other similar RL gyms, Isaac Gym can run simulations on the GPU and store results in GPU tensors rather than copying them back to CPU and memory. Also provides a Tensor-backed API to access these results, allowing RL observations and rewards calculations to also take place on GPU.

Isaac Gym also include a basic PPO implementation and a simple RL task system that can be used with it. Users may substitute alternative task systems and RL algorithms as desired.


## A. Installation via Conda

### Pre-requisites:
- Pyenv with Python 3.8
- Ubuntu 20.04


### A1. Setting up Isaac Gym:
1. Install Pyenv using the instructions provided [here](https://www.dedicatedcore.com/blog/install-pyenv-ubuntu/)
2. Install Miniconda by following the instructions [here](https://docs.anaconda.com/miniconda/). Don't forget to add miniconda to path, run `conda init` and `conda config --set auto_activate_base false`
3. Down the Isaac Gym repository from [here](https://developer.nvidia.com/isaac-gym)
4. Move the `isaacgym` folder to `$PROJECT_HOME/isaacgym`
5. Modify the `isaacgym/python/setup.py` and `isaacgym/python/isaacgym.egg-info/requires.txt` to have the following versions of libraries,
```
torch>=1.8.1,<=1.10.0,
torchvision=0.9.1,
numpy=1.18.5,
scipy=1.5.0,
pyyaml=6.0.2,
pillow,
imageio,
ninja,
```
6. Switch to `isaacgym` and run `./create_conda_env_rlgpu.sh` to create the conda environment and wait...this can take 15-30 mins depending on your internet speed.
    NOTE: Run `conda remove -n rlgpu --all` if you have an existing environment with the same name.
7. You now have a conda env named `rlgpu` with all the dependencies installed. Run `conda activate rlgpu` to activate this environment.
8. NOTE: For interacting with Isaac Gym, it is necessary to have `rlgpu` environment activated.
8. To test the Isaac Gym installation, run `cd isaacgym/python/examples && python joint_monkey.py` to watch a demo of a trained agent flexing all its joints.

### A2. Setting up Isaac Gym Envs:
IsaacGymEnvs is a collection of sample RL environments for Isaac Gym. It is built on top of deprecated version of [OpenAI Gym](https://www.gymlibrary.dev/content/basic_usage/) (moved to [`gymnasium`](https://gymnasium.farama.org/index.html)).

1. Clone `https://github.com/isaac-sim/IsaacGymEnvs.git`
2. Activate `rlgpu` conda ennvironment and run `pip install -e .` from inside the root of `IsaacGymEnvs` directory.

> **Tip:** Read the code of these examples and understand what they are trying to achieve. Try to modify the behaviour/policy/env a little bit and re-run the training code to see what happens. You are running a simulation, go crazy and tinker around!


### A3. Setting Go2 in Isaac Gym: (WIP)

1. Clone `https://github.com/unitreerobotics/unitree_rl_gym.git`
2. Create a Pyenv with Python 3.8 with `pyenv virtualenv 3.8 go2_gym` and activate with `pyenv activate go2_gym`
3. Switch to `isaacgym` directory and run `pip install -e .`. After activating the pyenv follow the steps 4 & 5 in section A1.
4. NOTE: Installing the same package versions is very important.
5. Come out of `unitree_rl_gym` repository and clone `https://github.com/leggedrobotics/rsl_rl`
6. Run `cd rsl_rl && git checkout v1.0.2 && pip install -e .`
7. Clone `https://github.com/unitreerobotics/unitree_rl_gym.git` (This is the main rl_gym repository for Unitree Go2)
8. Run `cd unitree_rl_gym && pip install -e .`
9. That's it! Now you are setup to run pretrained examples to test your setup. From `unitree_rl_gym` directory run `python legged_gym/scripts/train.py --task=go2`


## Troubleshooting
1. If you come across an error like `ImportError: /home/ubuntu/miniconda3/envs/rlgpu/lib/python3.8/site-packages/torch/lib/libtorch_cpu.so: undefined symbol: iJIT_NotifyEvent` then this is a problem due to torch install of conda not compiling the required platform libraries. To fix this, you can try running `pip install --force-reinstall torch==<version> torchvision==<version>` or remove these 2 package from conda and install them again using pip. pip also compiles the required platform libraries.
    - *NOTE:* Be careful as this can break your conda environment if not done properly.
2. If you come across erros related to numpy installation in the conda environment during setup or later then make the numpy version in `isaacgym/python/setup.py` and `isaacgym/python/isaacgym.egg-info/requires.txt` same as the one being installed using conda or pip. At the time of writing this, the versions were 1.18.5 were working.
```
Failed to build numpy
ERROR: ERROR: Failed to build installable wheels for some pyproject.toml based projects (numpy)
```
Fix: Align the numpy version in `setup.py` and `requires.txt` with the one being installed using conda or pip. At the time of writing this, the versions were 1.24.4 were working.
3. From the experiences, the most number of errors during setup are due to inconsistent/incompatible versions of the libraries and the dependencies. So, pay close attention to them and think calmly in a structured way when in this situation. DON'T BLINDLY COPY+PASTE COMMANDS FROM stackoverflow!
4. While installing `IsaacGymEnvs`, you might get an error related to minimum version of `pyyaml>=6.0` but `isaacgym` was installed with `5.3.1`. In this case, install required version of pyyaml with `pip install pyyaml==6.0.2` and then update this versin in the `setup.py` and `isaacgym.egg-info/requires.txt` of `isaacgym` directory. If you had already used the version mentioend above then you should fine for the time-being.
5. While installating `unitree_rl_gym`, if you have issues due to inconsistent pytorch versions then update the requirement of `isaacgym` to `torch>=1.8.1,<=1.10.0` and install the version required by `unitree_rl_gym` as mentioned in the repository.


### Isaac Sim/Lab/Gym References:
- [https://docs.robotsfan.com/isaacgym/install.html](https://docs.robotsfan.com/isaacgym/install.html)
- [PPO Algorithm - Policy Training for RL](https://medium.com/@danushidk507/ppo-algorithm-3b33195de14a)


### Go2 Reinforcement Learning Community Work:
- [https://github.com/Mehooz/vision4leg](https://github.com/Mehooz/vision4leg)
- [https://github.com/machines-in-motion/Go2Py](https://github.com/machines-in-motion/Go2Py)
- [https://github.com/eppl-erau-db/go2_rl_ws](https://github.com/eppl-erau-db/go2_rl_ws)
- [https://github.com/iit-DLSLab/Quadruped-PyMPC](https://github.com/iit-DLSLab/Quadruped-PyMPC)
- [https://youtu.be/9VJujzU8dDU?si=PpHJ_mUGjAZWp5hm](https://youtu.be/9VJujzU8dDU?si=PpHJ_mUGjAZWp5hm)
- [https://github.com/housework-robot/main](https://github.com/housework-robot/main)

You can read these repositories to gain better understanding for the customizations you are planning to do in your contributions.
