# Robotic Arm Teleoperation in Gazebo
This repository provides simulation and teleoperation tools for controlling a robotic arm in Gazebo using keyboard input and ROS controllers.

## Features
- **Keyboard Control**: Manual control of end-effector velocities.
- **Velocity Mapping**: Key-based directional velocity control.
- **Inverse Kinematics**: Joint velocities calculated using the Jacobian inverse.

## How to use this repo
### Prerequisites :
- #### Install Gazebo
  We will be launching our world in Gazebo so make sure to install it by using the command 
  ```
  curl -sSL http://get.gazebosim.org | sh
  ```
- #### Install ROS dependencies

  ```
  sudo apt-get install ros-noetic-gazebo-ros-pkgs ros-noetic-urdf ros-noetic-xacro ros-noetic-ros-control ros-noetic-ros-controllers
  ```
  For motion planning
  ```
  sudo apt-get install ros-noetic-moveit
  ```
  
> [!NOTE]
> All the installation commands are for rosdep noetic change noetic with <your_distro_name>

- #### Install ROS packages
  Make a workspace and create a directory 'src' where all the packages will be stored, clone this repo to get the packages and then build the catkin workspace.
  ```
  cd ~/robo_arm/src/
  git clone https://github.com/bhumii-ka/new_arm.git
  cd ~/robo_arm && catkin build
  ```
  Source your workspace in .bashrc file by running the following command so that you don't have to source it in every terminal
  ```
  echo "source ~/robo_arm/devel/setup.bash" >> ~/.bashrc
  ```

  ## Usage

  ### For IIWA Arm
  To start the Gazebo simulation:
  
  ```
  roslaunch iiwa_description l.launch
  ```
  To control the robotic arm via keyboard:
  
  ```
  roscd iiwa_description && cd urdf
  rosrun iiwa_description IK_gazebo.py
  ```
  ### For IIWA Arm through moveit
  To start the Gazebo simulation:
  
  ```
  roslaunch moveit_iiwa demo_gazebo.launch
  ```
  To start the Rviz without gazebo simulation:
  
  ```
  roslaunch moveit_iiwa demo.launch
  ```
  
  ### For XARM control
  #### Prerequisites
  In Gazebo simulator, navigate through the model database for 'table' item, drag and place the 3D model inside the virtual environment. It will then be downloaded locally, as 'table' is needed for running the demo.

  #### Control
  To start the Gazebo simulation:
  
  ```
  roslaunch xarm_gazebo xarm7_beside_table.launch add_gripper:=true
  ```
  To start the Rviz simulation:
  
  ```
  roslaunch xarm7_gripper_moveit_config xarm7_gripper_moveit_gazebo.launch
  ```
  To start teleoperation node
  ```
  rosrun xarm_gazebo IK_gazebo.py
  ```

  ### Keyboard Controls
  - `w` - Move +X
  - `s` - Move -X
  - `a` - Move +Y
  - `d` - Move -Y
  - `q` - Move +Z
  - `e` - Move -Z
  
  Press `Ctrl+C` to exit.
