# Checkpoint 17

<a name="readme-top"></a>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#software-prerequisites">Software Prerequisites</a></li>
        <li><a href="#hardware-prerequisites">Hardware Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage-simulation">Usage Simulation</a></li>
  </ol>
</details>


## About The Project
Repository for CI/CD based on Jenkins and a tortoisebot


<!-- GETTING STARTED -->
## Getting Started

### Software Prerequisites
* ROS Noetic
* Docker

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- INSTALLATION -->
### Installation
1. Clone the repo
   ```sh
   git clone https://github.com/mefisto2017/checkpoint17
   ```
2. Docker instalation
   ```sh
   sudo apt-get update
   sudo apt-get install docker.io docker-compose
   sudo service docker start
   ```
3. Docker configuration
   ```sh
   sudo usermod -aG docker $USER
   newgrp docker
   ```
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- USAGE of the simulation -->
## Usage Simulation
1. Launch the simulation and activate the controllers:
```sh
ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py
```

2. Move the robot:
```sh
ros2 topic pub --rate 10 /rb1_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.2}}"
```

3. Lift the platform:
```sh
ros2 topic pub --rate 10 /elevator_controller/commands std_msgs/msg/Float64MultiArray  "data:
- 10.0"
```

4. Lower the platform:
```sh
ros2 topic pub --rate 10 /elevator_controller/commands std_msgs/msg/Float64MultiArray  "data:
- -10.0"
```
