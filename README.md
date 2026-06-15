# pairs_uav_core (ROS 2)

Top-level **metapackage** for the **PAIRS UAV system** — a multirotor autonomy
stack for university-lab research, faithfully derived from the open-source
[CTU-MRS](https://github.com/ctu-mrs) `pairs_uav_core` (BSD-3-Clause).

This is the **ROS 2 Jazzy** (ament_cmake) line. The signed PAIRS apt repository
currently publishes the **ROS 1 Noetic** binaries; on ROS 2, build from source
(below) — Jazzy `.deb` / `bloom-release` packaging is in progress.

## Build from source (ROS 2 Jazzy)

Component repositories are pulled with [gitman](https://gitman.readthedocs.io):

```bash
# in your colcon workspace src/
git clone -b ros2 https://github.com/pairs-lab/pairs_uav_core.git
cd pairs_uav_core/ros_packages
gitman install            # clones all components on their ros2 branch into .gitman/
cd ~/colcon_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build
```

The core bring-up is `ros_packages/pairs_uav_core/launch/core.launch.py`.

## The stack

This metapackage aggregates the following PAIRS packages (see
[`ros_packages/.gitman.yml`](ros_packages/.gitman.yml)):

| Package | Role |
|---|---|
| [`pairs_msgs`](https://github.com/pairs-lab/pairs_msgs) | ROS messages & services |
| [`pairs_lib`](https://github.com/pairs-lab/pairs_lib) | shared C++ utility library |
| [`pairs_uav_hw_api`](https://github.com/pairs-lab/pairs_uav_hw_api) | hardware abstraction / autopilot bridge |
| [`pairs_uav_managers`](https://github.com/pairs-lab/pairs_uav_managers) | **control / estimation / constraint / gain / uav managers** + the controller/tracker/estimator plugin interfaces |
| [`pairs_uav_controllers`](https://github.com/pairs-lab/pairs_uav_controllers) | SE(3), MPC, failsafe, midair-activation controllers |
| [`pairs_uav_trackers`](https://github.com/pairs-lab/pairs_uav_trackers) | MPC / landoff / joy / speed reference trackers |
| [`pairs_uav_state_estimators`](https://github.com/pairs-lab/pairs_uav_state_estimators) | state estimation plugins |
| [`pairs_uav_trajectory_generation`](https://github.com/pairs-lab/pairs_uav_trajectory_generation) | time-optimal trajectory generation (eth + nlopt) |
| [`pairs_uav_autostart`](https://github.com/pairs-lab/pairs_uav_autostart) | automatic arming / takeoff |
| [`pairs_uav_status`](https://github.com/pairs-lab/pairs_uav_status) | ncurses terminal status display |
| [`pairs_rviz_plugins`](https://github.com/pairs-lab/pairs_rviz_plugins) | RViz visualization plugins |
| [`pairs_multirotor_simulator`](https://github.com/pairs-lab/pairs_multirotor_simulator) | lightweight multirotor dynamics simulator |
| [`pairs_uav_testing`](https://github.com/pairs-lab/pairs_uav_testing) | integration-test harness |

> **Note (MPC):** on ROS 2 the MPC controller/tracker also depend on a
> `pairs_mpc_solvers` package (the prebuilt MPC solver), which is not yet ported.

## Branches

- **`ros1`** — ROS 1 Noetic (catkin) — apt-installable via `ros-noetic-pairs-uav-core`
- **`ros2`** — ROS 2 Jazzy (ament_cmake) — *this branch*

## License

BSD-3-Clause. This is a rename-port of the CTU-MRS `pairs_uav_core`; the original
copyright is retained in [LICENSE](LICENSE) alongside the PAIRS copyright.
