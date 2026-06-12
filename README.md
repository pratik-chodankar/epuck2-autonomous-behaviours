# Autonomous Mobile Robot — e-puck2

**MSc Robotics | University of Sheffield | 2024-2025**

---

## What This Project Does

Implements three real-time autonomous behaviours on a physical e-puck2 mobile robot using C++ and ROS 2. All behaviours run on real hardware — not simulation only.

### Behaviour 1: Obstacle Avoidance
The robot navigates through an environment while detecting and avoiding obstacles in real time. Uses 8 infrared proximity sensors arranged around the robot body. When a sensor reading exceeds the detection threshold, the robot calculates a steering correction proportional to the sensor distance and direction, then adjusts wheel velocities accordingly.

### Behaviour 2: Bounded Exploration
The robot explores its environment systematically, covering as much area as possible while staying within defined boundaries. Uses a coverage-based strategy to bias movement toward unexplored regions, tracked via a local occupancy representation.

### Behaviour 3: Object Following
The robot detects a target object and follows it, maintaining a fixed following distance. Velocity is proportional to the measured range — faster when far, slower when close. The robot stops when within a minimum safe distance.

---

## Tech Stack

- C++ (primary implementation language)
- ROS 2 (Humble) — nodes, topics, and message passing
- RViz — real-time visualisation of sensor data and robot state
- URDF — robot model definition
- e-puck2 physical hardware
- Infrared proximity sensor array (8 sensors)
- Differential drive actuators

---

## Repository Structure

```
epuck2-autonomous-behaviours/
├── src/
│   ├── obstacle_avoidance.cpp   - Obstacle avoidance behaviour
│   ├── exploration.cpp          - Bounded exploration behaviour
│   ├── object_following.cpp     - Object following behaviour
│   └── sensor_utils.cpp        - Proximity sensor reading and processing
├── include/
│   ├── obstacle_avoidance.h
│   ├── exploration.h
│   ├── object_following.h
│   └── sensor_utils.h
├── urdf/
│   └── epuck2.urdf              - Robot model for RViz visualisation
├── launch/
│   ├── obstacle_avoidance.launch.py
│   ├── exploration.launch.py
│   └── object_following.launch.py
├── config/
│   └── sensor_thresholds.yaml  - Configurable detection thresholds
└── README.md
```

---

## How to Build and Run

### Requirements
- ROS 2 Humble
- Ubuntu 22.04
- e-puck2 hardware (or Gazebo simulation)

### Build
```bash
cd ~/ros2_ws/src
git clone https://github.com/33hacker33/epuck2-autonomous-behaviours
cd ~/ros2_ws
colcon build --packages-select epuck2_behaviours
source install/setup.bash
```

### Run obstacle avoidance
```bash
ros2 launch epuck2_behaviours obstacle_avoidance.launch.py
```

### Run exploration
```bash
ros2 launch epuck2_behaviours exploration.launch.py
```

### Run object following
```bash
ros2 launch epuck2_behaviours object_following.launch.py
```

### Visualise in RViz
```bash
ros2 run rviz2 rviz2 -d config/epuck2_view.rviz
```

---

## Sensor Configuration

The e-puck2 has 8 infrared proximity sensors positioned around its body:

```
        Front
    [7]  [0]  [1]
  [6]          [2]
    [5]  [4]  [3]
        Back
```

Sensors 0-2 cover the front arc and are the primary inputs for obstacle avoidance. All 8 sensors contribute to exploration boundary detection.

---

## Related

- [swarm-robotics-kilobot](https://github.com/33hacker33/swarm-robotics-kilobot) — multi-agent path planning
- [sensor-fusion-ekf](https://github.com/33hacker33/sensor-fusion-ekf) — state estimation and localisation
- LinkedIn: [pratik-chodankar200114](https://www.linkedin.com/in/pratik-chodankar200114)
