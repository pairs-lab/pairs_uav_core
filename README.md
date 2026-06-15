# pairs_uav_core

Top-level **metapackage** for the PAIRS UAV system, a multirotor autonomy stack
for university-lab research. It does not contain any flight code of its own;
instead it depends on every component of the stack so that installing this one
package pulls in the whole thing: messages, the shared library, the hardware API,
the managers, controllers, trackers, state estimators, trajectory generation,
autostart, status display, RViz plugins, and the lightweight simulator. It also
ships the core bring-up launch files that wire those managers together for a UAV.

## Contents

- `launch/core.launch` — brings up the full per-UAV control stack (control / estimation / transform / constraint / gain / UAV managers, plus trajectory generation and status).
- `launch/nodelet_manager.launch` — the shared nodelet manager.
- `launch/rviz.launch` — RViz with the default PAIRS configuration.

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
| [`pairs_rviz_plugins`](https://github.com/pairs-lab/pairs_rviz_plugins) | RViz visualization plugins |
| [`pairs_multirotor_simulator`](https://github.com/pairs-lab/pairs_multirotor_simulator) | lightweight multirotor dynamics simulator |
| [`pairs_uav_testing`](https://github.com/pairs-lab/pairs_uav_testing) | integration-test harness |

## Branches

- `ros1` — ROS 1 Noetic (catkin)
- `ros2` — ROS 2 Jazzy (ament_cmake)

## Install (ROS 1 Noetic)

```bash
sudo apt install ros-noetic-pairs-uav-core
```

Individual packages can also be installed by name, e.g.
`sudo apt install ros-noetic-pairs-uav-controllers`.

## Build from source

The component repositories are pulled with [gitman](https://gitman.readthedocs.io):

```bash
# in your catkin workspace src/
git clone -b ros1 https://github.com/pairs-lab/pairs_uav_core.git
cd pairs_uav_core/ros_packages
gitman install            # clones all components on their ros1 branch into .gitman/
cd ~/catkin_ws
catkin build
```

## Usage

```bash
roslaunch pairs_uav_core core.launch
```

`core.launch` expects the `UAV_NAME` and `RUN_TYPE` environment variables to be
set and is normally invoked from a simulation or real-world bring-up session.

## License

BSD-3-Clause. This is a rename-port of the CTU-MRS `pairs_uav_core`; the original
copyright is retained in [LICENSE](LICENSE) alongside the PAIRS copyright.
