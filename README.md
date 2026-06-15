# pairs_uav_core

Top-level **metapackage** for the PAIRS UAV system, a multirotor autonomy stack
for university-lab research. This is the **ROS 2 Jazzy** (ament_cmake) line. It
contains no flight code of its own; it depends on every component of the stack so
that building it brings in the whole thing, and it ships the core bring-up launch
file that wires the managers together for a UAV.

## Contents

- `launch/core.launch.py` — brings up the full per-UAV control stack.

## The stack

This metapackage aggregates the following PAIRS packages (managed as gitman
submodules in [`ros_packages/.gitman.yml`](ros_packages/.gitman.yml)):

| Package | Role |
|---|---|
| [`pairs_msgs`](https://github.com/pairs-lab/pairs_msgs) | ROS messages & services |
| [`pairs_lib`](https://github.com/pairs-lab/pairs_lib) | shared C++ utility library |
| [`pairs_uav_hw_api`](https://github.com/pairs-lab/pairs_uav_hw_api) | hardware abstraction / autopilot bridge |
| [`pairs_uav_managers`](https://github.com/pairs-lab/pairs_uav_managers) | control / estimation / constraint / gain / uav managers + the controller/tracker/estimator plugin interfaces |
| [`pairs_uav_controllers`](https://github.com/pairs-lab/pairs_uav_controllers) | SE(3), MPC, failsafe, midair-activation controllers |
| [`pairs_uav_trackers`](https://github.com/pairs-lab/pairs_uav_trackers) | MPC / landoff / joy / speed reference trackers |
| [`pairs_uav_state_estimators`](https://github.com/pairs-lab/pairs_uav_state_estimators) | state estimation plugins |
| [`pairs_uav_trajectory_generation`](https://github.com/pairs-lab/pairs_uav_trajectory_generation) | time-optimal trajectory generation |
| [`pairs_uav_autostart`](https://github.com/pairs-lab/pairs_uav_autostart) | automatic arming / takeoff |
| [`pairs_uav_status`](https://github.com/pairs-lab/pairs_uav_status) | terminal status display |
| [`pairs_multirotor_simulator`](https://github.com/pairs-lab/pairs_multirotor_simulator) | lightweight multirotor dynamics simulator |
| [`pairs_uav_testing`](https://github.com/pairs-lab/pairs_uav_testing) | integration-test harness |

## Branches

- `ros1` — ROS 1 Noetic (catkin)
- `ros2` — ROS 2 Jazzy (ament_cmake)

## Install (ROS 2 Jazzy)

```bash
sudo apt install ros-jazzy-pairs-uav-core
```

## Build from source

The component repositories are pulled with [gitman](https://gitman.readthedocs.io):

```bash
# in your colcon workspace src/
git clone -b ros2 https://github.com/pairs-lab/pairs_uav_core.git
cd pairs_uav_core/ros_packages
gitman install            # clones all components on their ros2 branch into .gitman/
cd ~/colcon_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build
```

## Usage

```bash
ros2 launch pairs_uav_core core.launch.py
```

## License

BSD-3-Clause. This is a rename-port of the CTU-MRS `pairs_uav_core`; the original
copyright is retained in [LICENSE](LICENSE) alongside the PAIRS copyright.
