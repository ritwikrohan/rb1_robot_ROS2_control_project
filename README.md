# RB-1 ROS2 Control Package

## rb1_ros2_description Package
This ROS2 package is designed to simulate the RB1 robot and provides a detailed robot description for use in ROS2 environments. The package includes a differential drive and effort controller to enable users to simulate and control the RB1 robot's movement. Differential drive controller is used to move the robot and elevator effort controller is used to lift the elevator up or down.

## Installation Instructions

To use this package, follow these installation instructions:

## 1. Change your directory to your ROS2 Workspace
  ```bash
  cd ~/your_ros2_workspace/src
  ```

## 2. Clone the repository into your ROS workspace:

   ```bash
   git clone https://github.com/ritwikrohan/rb1_robot_control_project.git
   ```
## 3. Build the workspace
  ```bash
  cd ~/your_ros2_workspace && colcon build && source install/setup.bash
  ```
# Running Simulations

## 1. Launch the gazebo node with ROS2 controllers using the following command: (Note that you will have to wait a bit (approximately 100 seconds or less) for gazebo plugins to be loaded)
  ```bash
  ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py
  ```
## 2. Now check if the controllers are activated or not. Use the following command in a separate terminal (make sure you source your workspace):
  ```bash
  ros2 control list_controllers
  ```
  you Should see this output if the controllers are successfully activated otherwise close the gazebo node and relaunch using step 1 of Running Simulations:
  ```bash
  joint_state_broadcaster[joint_state_broadcaster/JointStateBroadcaster] active
  rb1_base_controller [diff_drive_controller/DiffDriveController] active
  elevator_effort_controller[effort_controllers/JointGroupEffortController] active
  ```
# Controlling the robot
## Moving the robot

## 1. You can use ros2 teleop to control the robot movement using keyboard. Use the following command in a separate terminal:
  ```bash
  ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap cmd_vel:=/rb1_base_controller/cmd_vel_unstamped
  ```
## 2. You can also publish on topic to move the robot. Use the following command in a separate terminal:
  ```bash
  ros2 topic pub --rate 10 /rb1_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.2}}"
  ```

## Lifting the elevator (Up/Down)

## 1. To lift up the elevator of the robot publish on the topic only once. Use the following command in a separate terminal:
  ```bash
  ros2 topic pub /elevator_effort_controller/commands std_msgs/msg/Float64MultiArray "{data: [10.0]}" -1
  ```
## 2. To lower the elevator down, use the same topic for publishing once. Use the following command in a separate terminal:
  ```bash
   ros2 topic pub /elevator_effort_controller/commands std_msgs/msg/Float64MultiArray "{data: [0.0]}" -1
  ```
  


