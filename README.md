# Learn Isaac Lab
Repository for getting started and learning Isaac Lab - robotics simulation framework by NVIDIA.

## Overview
Isaac Sim provides a powerful robotics simulation environment built on NVIDIA's Omniverse platform. This repository contains examples and tutorials to help you get started with robot simulation, training, and sim-to-real transfer.

## Installation & Setup

### Prerequisites
- NVIDIA GPU with driver version 525.60.13 or later
- Ubuntu 22.04
- Python 3.8+
- 32GB+ RAM recommended
- 16GB VRAM recommended

### Install via Docker
1. Install Docker for your OS. You can refer to [installation steps here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)
2. Install Docker Compose for you OS. You can refer to the [installation steps here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)
3. Tip: Don't forget to run the Docker post-installation in #1. This provides the necessary permissions for the Docker service to run without sudo.
4. To build and run GPU accelerated containers, install NVIDIA Container Toolkit using the instructions provided [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) (prefer using `apt` if you are on Ubuntu).
5. **NOTE:** Make sure the Isaac Lab directory is placed under `/home` directory tree when using Docker.

### Obtaining the Isaac Sim Container
1. Get the Isaac Sim Container from [here](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/isaac-sim)
2. Get your NVIDIA GPU Cloud (NGC) API key using the instructions [here](https://docs.nvidia.com/ngc/gpu-cloud/ngc-user-guide/index.html#generating-api-key)
3. Install NGC CLI using the instructions [here](https://org.ngc.nvidia.com/setup/installers/cli)
4. Set up NGC CLI with `ngc config set`
4. Input the Username (`$oauthtoken`) and API Key (`YnN2cGdiNGE2Mjlzbzlmb3FmcjJxZjRncHQ6MjQ5NzkyNzEtZjlhYi00MDU0LWJhOTgtOTFlOGNmYjViMTUx`) in `docker login nvcr.io`

### Understaind the `docker` directory in `isaac-sim/IsaacLab`
This directory contains the files and scripts required to run Isaac Lab inside a Docker container. Following are the high level explanations of few such files,
- `Dockerfile.base` - Defines the base Isaac Lab image by overlaying the necessary dependencies onto to the Isaac Sim Docker image. Dockerfiles ending an extension (like `Dockerfile.ros2`) build an image extension instead. Check the Dockerfiles to understand the differences in these environments.
- `docker-compose.yaml` - Create volume mounts to allow direct editing of Isaac Lab code from the host machine that runs the container. It also creates support volumes such as `isaac-cache-kit` to store frequently re-used resources compiled by Isaac Sim like shaders, to retain logs, data and documents.
- `.env.base` - Stores environment variables required for the `base` build process and the container itself. `.env` files ending with other extensions (like `.ros2`) define these for image extensions.
- container.py - Utility script that interfaces with tools in `docker/utils` directory to configure and build the image, run and interact with the container in headless or GUI(X11) mode.

#### IMPORTANT: 
For Go2, it is important to change the DDS middleware used by ROS2 Humble Docker image to CycloneDDS. To achieve this, make the following changes to `/isaac-sim/IsaacLab/docker/.env.ros2`,
```
# Update this env variable to use CycloneDDS instead of Fast-RTPS
RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```
### Running the Container
TBA


### Install via pip


## Running Simulations

### Basic Usage (WIP
TBA

### Examples
- Basic robot control
- Environment interaction
- Sensor integration
- Physics simulation

## Training (WIP)

### Reinforcement Learning
- Integration with popular RL frameworks
- Example training scripts
- Hyperparameter configurations

### Synthetic Data Generation
TBA

## Deployment (WIP)

### Sim-to-Real Transfer
TBA

### Real Robot Integration (WIP)
- ROS/ROS2 bridge
- Hardware communication
- Calibration procedures
