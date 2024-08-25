# ROS 2 Environment with Mujoco


The following repository ROS 2 environment with [Mujoco](https://mujoco.org/) - advanced physics simulator.

## Build


```bash

sudo ./build.sh

```


## Run

```bash

sudo ./run.sh

```

```bash
source install/setup.bash

ros2 launch mujoco_ros2_control_demos cart_example_position.launch.py

or

ros2 launch mujoco_ros2_control_demos diff_drive.launch.py
```

```bash
# Launch other terminal

source install/setup.bash

rqt
```

![image](https://github.com/user-attachments/assets/0c720c01-bd2c-4e9b-a4d8-2ceec33101f7)


![image](https://github.com/user-attachments/assets/3032c9ca-cd39-4291-80ba-9ec4dba189da)


## Run Mujoco 

```bash

cd /home/mujoco/mujoco-3.2.2/bin

./simulate ../model/humanoid/humanoid.xml
```
![image](https://github.com/user-attachments/assets/95a41995-ee8a-48d7-ad69-8cffee9ec3dc)


## Acknowledgment

- [mujoco_ros2_control](https://github.com/sangteak601/mujoco_ros2_control)
- [Mujoco documentation](https://mujoco.readthedocs.io/en/latest/overview.html)
