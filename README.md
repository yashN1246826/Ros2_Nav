````md
# ROS2 Autonomous Navigation Simulation

A ROS2 and Gazebo-based robotics simulation project demonstrating autonomous navigation, object detection, traffic-rule behaviour, obstacle avoidance and landmark logging in a simulated maze environment.

This project was developed as part of my robotics/computer science coursework to show how a mobile robot can use sensor data, object detection and navigation logic to move through an environment and respond to real-world style signs such as stop, slow and fast signs.

---

## Project Overview

The system simulates a robot navigating through a Gazebo maze world using ROS2. The robot processes sensor and camera data, detects objects/signs using a YOLO-based detection pipeline, follows traffic-rule behaviours, avoids obstacles and records detected landmarks with estimated positions.

The project combines robotics simulation, computer vision, navigation logic and ROS2 communication using topics, nodes and messages.

---

## Key Features

- ROS2-based robot simulation using Gazebo
- Autonomous navigation in a maze environment
- YOLO-based traffic sign and object detection
- Traffic-rule behaviour:
  - Stop sign detection
  - Slow sign speed reduction
  - Fast sign speed increase
- Obstacle-aware navigation using odometry and sensor data
- Landmark detection and logging
- ROS2 topic-based communication between nodes
- Docker/Linux-based development environment
- TF/odometry frame handling for robot localisation support

---

## Tech Stack

- **ROS2 Humble**
- **Gazebo / Ignition Gazebo**
- **Python**
- **C++**
- **CMake**
- **Shell scripting**
- **YOLO object detection**
- **Docker**
- **Linux**
- **RViz / ROS visualisation tools**

---

## System Architecture

The project is structured around several ROS2 nodes that communicate using topics.

Typical data flow:

```text
Gazebo Simulation
        ↓
Robot Camera / Sensor Topics
        ↓
YOLO Object Detection
        ↓
Traffic Sign / Landmark Detection
        ↓
Navigation and Behaviour Logic
        ↓
Velocity Commands to Robot
````

The robot receives camera and odometry data from the simulation, detects objects/signs, applies behaviour rules and publishes movement commands.

---

## Main Components

### 1. Simulation Environment

The robot is launched inside a Gazebo maze environment. The world contains objects, traffic signs and landmarks that the robot must detect and respond to.

### 2. Object Detection

A YOLO-based detection pipeline is used to identify objects and traffic signs from the robot camera feed.

Detected signs can include:

* Stop sign
* Slow sign
* Fast sign
* Landmarks / objects in the environment

### 3. Traffic Rule Behaviour

The robot changes its movement depending on the detected sign:

| Sign Detected     | Robot Behaviour                            |
| ----------------- | ------------------------------------------ |
| Stop sign         | Robot stops for a short duration           |
| Slow sign         | Robot reduces speed                        |
| Fast sign         | Robot increases speed                      |
| Obstacle detected | Robot adjusts direction to avoid collision |

### 4. Navigation Logic

The navigation system uses odometry and sensor information to move through the maze. The robot can detect obstacles and decide whether to continue forward, turn or recover from a blocked path.

### 5. Landmark Logging

Detected landmarks are stored with useful information such as:

* Landmark class
* Estimated position
* Confidence score
* Observation count
* Timestamp

This allows the robot to build a basic record of important objects found in the environment.

---

## Repository Structure

```text
Ros2_Nav/
│
├── src/                 # Main ROS2 source packages
├── build/               # Build output files
├── install/             # Installed ROS2 workspace files
├── log/                 # ROS2 build/runtime logs
├── frames_*.pdf         # TF frame visualisation outputs
├── frames_*.gv          # Graphviz TF frame files
└── README.md
```

> Note: In a production repository, `build/`, `install/` and `log/` are usually excluded using `.gitignore`.

---

## Example ROS2 Topics

Some of the topics used in this project include:

```text
/atlas/rgbd_camera/image
/yolo/detections
/atlas/odom_ground_truth
/atlas/cmd_vel
/atlas/cmd_vel_raw
/landmark_summary
/detected_goal
/all_detected_goals
```

These topics allow the robot to receive sensor data, process detections and publish movement/navigation commands.

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/yashN1246826/Ros2_Nav.git
cd Ros2_Nav
```

### 2. Source ROS2

```bash
source /opt/ros/humble/setup.bash
```

### 3. Build the workspace

```bash
colcon build
```

### 4. Source the workspace

```bash
source install/setup.bash
```

### 5. Launch the simulation

```bash
ros2 launch ntu_robotsim cwmaze.launch.py
```

### 6. Run project nodes

Example:

```bash
ros2 run <package_name> <node_name>
```

Replace `<package_name>` and `<node_name>` with the relevant package and node names from the `src/` folder.

---

## Example Commands

Check active ROS2 topics:

```bash
ros2 topic list
```

View camera/image topic:

```bash
ros2 topic echo /atlas/rgbd_camera/image
```

Check detections:

```bash
ros2 topic echo /yolo/detections
```

Check odometry:

```bash
ros2 topic echo /atlas/odom_ground_truth
```

Publish a test velocity command:

```bash
ros2 topic pub /atlas/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.2}, angular: {z: 0.0}}"
```

View TF frames:

```bash
ros2 run tf2_tools view_frames
```

---

## Results

The system demonstrates a working robotics pipeline where a simulated robot can:

* Navigate inside a maze world
* Detect traffic signs and objects
* Modify movement based on detected signs
* Avoid obstacles using sensor feedback
* Log detected landmarks
* Use ROS2 topics for modular communication between nodes

This project helped me gain practical experience in robotics software development, ROS2 communication, simulation environments, perception pipelines and autonomous navigation behaviour.

---

## Skills Demonstrated

* Robotics software development
* ROS2 node design
* Topic-based communication
* Gazebo simulation
* Computer vision integration
* YOLO object detection
* Navigation and obstacle avoidance logic
* Linux/Docker development workflow
* Debugging robotics systems
* Sensor and odometry handling

---

## Future Improvements

* Add a full Nav2 navigation stack integration
* Improve path planning with costmaps
* Add better obstacle recovery behaviour
* Improve landmark position estimation
* Add a dashboard for visualising detections and navigation state
* Improve documentation with screenshots and demo videos
* Add launch files for easier setup

---

## Author

**Yash Kumar**
Final-year Computer Science student interested in software engineering, robotics, AI, computer vision and cloud systems.

GitHub: [yashN1246826](https://github.com/yashN1246826)

````

Also, important: your repo currently includes `build`, `install`, and `log` folders. For GitHub, that looks messy. After adding README, create a `.gitignore` file and add:

```gitignore
build/
install/
log/
*.pyc
__pycache__/
.DS_Store
````

Then your repository will look much more professional.
