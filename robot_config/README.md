# Robot Configuration Package

This package contains all centralized configuration files for the mobile manipulator robot.

## Configuration Files

### Controllers
- **frbot_controllers.yaml** - Controller configuration for real hardware
- **frbot_controllers_sim.yaml** - Controller configuration for Gazebo simulation
  - diff_drive_controller: Mobile base control
  - arm_controller: 4-DOF manipulator arm control (joint_trajectory_controller)

### Sensors
- **imu_config.yaml** - IMU sensor configuration (BNO055 or similar)
- **velodyne_config.yaml** - Velodyne LiDAR configuration (VLP-16)
- **realsense_config.yaml** - Intel RealSense camera configuration (D405/D435)

### Localization
- **ekf.yaml** - Extended Kalman Filter configuration for sensor fusion
  - Fuses odometry and IMU data
  - Publishes /odometry/filtered topic

### Gazebo Bridge
- **gz_ros_bridge.yaml** - Gazebo to ROS2 topic bridge configuration

## Usage

In your launch files:

```python
from ament_index_python.packages import get_package_share_directory

robot_config_pkg = get_package_share_directory("robot_config")
controllers_file = os.path.join(robot_config_pkg, "config", "frbot_controllers_sim.yaml")
```

## File Organization

```
robot_config/
├── config/
│   ├── frbot_controllers.yaml        # Real hardware controllers
│   ├── frbot_controllers_sim.yaml    # Simulation controllers
│   ├── imu_config.yaml               # IMU sensor config
│   ├── velodyne_config.yaml          # LiDAR config
│   ├── realsense_config.yaml         # Camera config
│   ├── ekf.yaml                      # Localization config
│   └── gz_ros_bridge.yaml            # Gazebo bridge
├── CMakeLists.txt
├── package.xml
└── README.md
```

## Migration Notes

Configuration files were consolidated from:
- `robot_description/config/` → Controllers moved here
- `robot_gazebo/config/` → Gazebo bridge moved here
- `frbot_localization/config/` → EKF config moved here
- New sensor configs added: IMU, Velodyne, RealSense

All launch files have been updated to use this centralized package.
