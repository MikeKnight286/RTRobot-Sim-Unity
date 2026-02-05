
# Project Setup Documentation

## Overview
This documentation guides you through setting up a Docker container for ROS Noetic version, managing directories, building the workspace, creating packages, and running Python scripts within a ROS package.

## Prerequisites
- Docker installed on your machine
- Basic knowledge of Docker and ROS

## Setup Instructions

### Step 1: Setting Up the Docker Container
- **Environment**: Windows - Terminal 
- To dock local file from your desktop to docker container with two ports 6080:80 and 10000:10000 for ROS noetic version:
  ```
  docker run -v <working directory>\<local file name>:/home/ubuntu/catkin_ws:cached -p 6080:80 -p 10000:10000 --shm-size=1024m tiryoh/ros-desktop-vnc:noetic
  ```
- **Access Virtaul Machine**: Click on port 6080:80 in container or type `http://localhost:6080` in your browser and access LXTerminal.

### Step 2: Create Directory for Workspace
- **Command**:
  ```
  mkdir -p ~/catkin_ws/src
  ```

### Step 3: Build and Setup Workspace
- **Commands**:
  ```
  cd ~/catkin_ws
  catkin build
  source ~/catkin_ws/devel/setup.bash
  ```

### Step 4: Auto-run Setup Script
- **Command**:
  ```
  echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
  ```

### Step 5: Create Packages
- **Command**:
  ```
  cd ~/catkin_ws/src
  catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
  ```
  Example: `catkin_create_pkg test_tutorial rospy std_msgs`

### Step 6: Set Executable Permissions
- **Commands**:
  ```
  cd ~/catkin_ws/src/<package_name>/src
  chmod u+x *.py
  ```

### Step 7: Rebuild Workspace
- Redo Step 3.

### Step 8: Run Python Files
- **Commands**:
  ```
  roscore
  rosrun <package_name> <python_file.py>
  ```
  Note: Make sure to change to Linux line endings in editor for Python files (CRLF ---> LF).

## Additional Notes
- Ensure you replace placeholders like `<package_name>` and `<python_file.py>` with actual names relevant to your project.
- Red arow ROS IP in Unity means ROS server is not connected yet, so you need to connect the server again.
- If you want to stop the movement, stop either publish or subscribe terminal.

## To open server
- **Commands**:
  ```
  roscore
  (open new terminal and type)rosparam set ROS_IP 0.0.0.0
  rosrun ros_tcp_endpoint default_server_endpoint.py 
  ```
## If there is an error like this: /usr/bin/env: ‘python’: No such file or directory 
- **Commands**:
  ```
  1. sudo apt-get install python3 
  2. Open code file and replace: #!/usr/bin/env python as #!/usr/bin/env python3  
  ```
