# pairs_uav_core

Top-level **metapackage** for the **PAIRS UAV system** — a multirotor autonomy
stack for university-lab research, faithfully derived from the open-source
[CTU-MRS](https://github.com/ctu-mrs) `mrs_uav_core` (BSD-3-Clause).

Installing this one package pulls in the entire flight stack: estimation,
control, trajectory generation, hardware API, simulation, and bring-up tooling.

## Install (ROS 1 Noetic)

```bash
# 1. add the signed PAIRS apt repository
curl -fsSL https://thanhnguyencanh.github.io/apt/KEY.gpg \
  | sudo gpg --dearmor -o /usr/share/keyrings/pairs.gpg
echo "deb [signed-by=/usr/share/keyrings/pairs.gpg] https://thanhnguyencanh.github.io/apt noetic main" \
  | sudo tee /etc/apt/sources.list.d/pairs.list

# 2. install the whole stack
sudo apt update
sudo apt install ros-noetic-pairs-uav-core
```

Individual packages can also be installed by name, e.g.
`sudo apt install ros-noetic-pairs-uav-controllers`.

> For headless / scripted installs, prefix with `DEBIAN_FRONTEND=noninteractive`
> to skip the `keyboard-configuration` prompt pulled in transitively.

## The stack

This metapackage aggregates the following PAIRS packages (managed as gitman
submodules in [`ros_packages/.gitman.yml`](ros_packages/.gitman.yml)):

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

The core bring-up launch files live in
[`ros_packages/pairs_uav_core/launch`](ros_packages/pairs_uav_core/launch)
(`core.launch`, `nodelet_manager.launch`, `rviz.launch`).

## Branches

- **`ros1`** — ROS 1 Noetic (catkin) — *apt-installable today*
- **`ros2`** — ROS 2 Jazzy (ament_cmake)

## License

BSD-3-Clause. This is a rename-port of the CTU-MRS `mrs_uav_core`; the original
copyright is retained in [LICENSE](LICENSE) alongside the PAIRS copyright.

Maintainer: **Thanh Nguyen Canh** &lt;canhthanh@vnu.edu.vn&gt;
