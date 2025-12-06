# ros2_wheeltec_n100_imu

ROS2 driver for WHEELTEC N100 IMU module - **ROS2 Jazzy Compatible**

![alt wheeltec N100](https://i.ebayimg.com/images/g/2EsAAOSw7WVhk2Vr/s-l1600.jpg)

## About This Fork

This is a maintained fork with fixes and improvements for ROS2 Jazzy compatibility.

**Original Author**: [Nipun Dhananjaya](https://github.com/NDHANA94/ros2_wheeltec_n100_imu)
**Based on**: [ROS1 fdilink imu driver](https://github.com/sbgisen/fdilink_ahrs)

### Improvements in This Fork

- **ROS2 Jazzy Compatibility**: Tested and working on ROS2 Jazzy
- **Critical Bug Fix**: Fixed covariance parameters not being stored (lines 53-55 in imu_node.cpp)
- **Missing Dependency**: Added `geometry_msgs` to build dependencies
- **Clean Compilation**: Fixed all compiler warnings (12+ unused variable warnings)
- **Code Quality**: Removed unused code and improved maintainability
- **Stable Operation**: No more segmentation faults, proper data streaming

topics:
- /imu
- /imu_trueEast
- /magnetic_field
- /magnetic_pose_2d

### install
```
mkdir -p /ros2_ws/src
cd /ros2_ws/src
git clone https://github.com/RoverRobotics-forks/serial-ros2.git #install ros2_serial
git clone https://github.com/NDHANA94/ros2_wheeltec_n100_imu.git
cd ~/ros2_ws
colcon build
source install/setup.bash

```
### run

* defaut run:
default serial port: `/dev/ttyACM0`
default serial baudrate: `921600`
```
ros2 run wheeltec_n100_imu imu_node 
```

* run with custom params:
```
ros2 run wheeltec_n100_imu imu_node --ros-args -p serial_port:="/dev/ttyACM0" -p serial_baud:=921600
```

| parameter | data type | default value |
| --- | --- | --- |
| debug | bool | false |
|serial_port | string |  "/dev/ttyACM0" |
|serial_baud | int | 921600 |
|serial_timeout | int | 20 |
| device_type |int | 1 |
| frist_sn | bool | false |
| imu_topic | string | "imu" |
| imu_frame imu | string | "imu" |
| mag_pose_2d_topic | string |"magnetic_pose_2d" |
| imu_trueEast_topic | string | "imu_trueEast"|
| mag_topic | string | "magnetic_field" |
| yaw_offset | double | -2.094 |
| mag_offset_x | double | 0.0 |
| mag_offset_y | double | 0.0 |
| mag_offset_z | double | 0.0 |
| imu_mag_covVec | vector<double> | {0.01, 0.01, 0.01}|
| imu_gyro_covVec | vector<double> |  {0.01, 0.01, 0.01} |
| imu_accel_covVec | vector<double> |  {0.05, 0.05, 0.05} |

## Tested Platforms

- **OS**: Ubuntu 24.04 (Noble)
- **ROS2**: Jazzy Jalisco
- **Hardware**: Raspberry Pi 5, Wheeltec N100 IMU
- **Serial Interface**: USB (/dev/ttyUSB0) @ 921600 baud

## Visualization with Foxglove

This driver works seamlessly with [Foxglove Studio](https://foxglove.dev/):

1. Install Foxglove bridge:
   ```bash
   sudo apt install ros-jazzy-foxglove-bridge
   ```

2. Run the bridge:
   ```bash
   ros2 launch foxglove_bridge foxglove_bridge_launch.xml
   ```

3. Connect from browser at `ws://<your-robot-ip>:8765`

4. Add panels to visualize IMU data:
   - **Plot Panel**: Real-time graphs of orientation, velocity, acceleration
   - **Raw Messages**: View all IMU data fields
   - **3D Panel**: Visualize orientation (requires TF transforms)

## Troubleshooting

### Serial Port Permissions
If you get permission denied errors:
```bash
sudo usermod -aG dialout $USER
# Log out and log back in
```

### Topics Not Publishing
Check if IMU is detected:
```bash
ls -l /dev/ttyUSB* /dev/ttyACM*
```

Enable debug mode to see packet data:
```bash
ros2 run wheeltec_n100_imu imu_node --ros-args -p debug:=true
```

## Credits

- **Original ROS2 Port**: [Nipun Dhananjaya](https://github.com/NDHANA94)
- **ROS1 Base**: [fdilink_ahrs by sbgisen](https://github.com/sbgisen/fdilink_ahrs)
- **Jazzy Fixes**: This fork

## License

Same as original project (check LICENSE file)

