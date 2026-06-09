# pairs_uav_core

Top-level **PAIRS UAV** metapackage / aggregator — a faithful rename-port of the
CTU-MRS `mrs_uav_core`. It depends on the full PAIRS UAV stack and provides the
core bring-up launch files (`ros_packages/pairs_uav_core/launch`).

Component repositories are managed via `ros_packages/.gitman.yml`
(`gitman install`), pointing at `github.com/pairs-lab/pairs_*` on the `ros2` branch.

## Branches
- `ros1` — ROS 1 Noetic (catkin)
- `ros2` — ROS 2 Jazzy (ament_cmake)

## License
BSD 3-Clause. Derived from the CTU-MRS `mrs_uav_core`; original copyright retained
in [LICENSE](LICENSE). Maintainer: Thanh Nguyen Canh <canhthanh@vnu.edu.vn>
