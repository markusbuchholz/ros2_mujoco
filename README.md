## ROS 2 Environment with Mujoco


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
```

```bash
# Launch other terminal

source install/setup.bash

rqt
```
