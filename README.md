# 🧠 Puzzlebot ROS 2 Navigation Stack (Nav2 + SLAM)

This repository contains the ROS 2 packages developed to integrate the **Navigation2 (Nav2) stack** with the **MCR2 Puzzlebot**, including simulation, SLAM, and the base navigation pipeline.


## 📌 Team Members

- Jose (GitHub: Agui6106, Aguilar-606)
- Pau (GitHub: PaulinaLopezC)
- Isra (Github: IsraSa)
- Ricard (GitHub: Ric4rd1)

## ⚙️ Requirements

Make sure you have the following installed:

- ROS 2 (Humble recommended)
- Nav2
- SLAM Toolbox
- Gazebo (Garden / Fortress depending on setup)
- RViz2

### Install dependencies:

```bash
sudo apt update
rosdep update
rosdep install --from-paths src --ignore-src -r -y
```
---

## 📁 Repository Structure

```bash
puzzlebot_ws/
└── src/
    └── puzzlebot_ros2/
        ├── puzzlebot_description/
        ├── puzzlebot_gazebo/
        └── puzzlebot_navigation2/
```


## 📦 Packages Description

### 🔹 `puzzlebot_description`

This package contains the **robot model definition** for the Puzzlebot. It includes all the elements required to describe the robot both visually and physically.

**Main responsibilities:**
- Define the robot structure using URDF/Xacro
- Specify frames (`base_link`, `base_footprint`, etc.)
- Include sensor definitions (e.g., LiDAR)
- Provide collision and visual models
- Enable visualization in RViz

**Key contents:**
- `urdf/` → Modular Xacro/URDF files
- `meshes/` → 3D models of the robot
- `rviz/` → RViz configuration for visualization
- `launch/` → Launch file to load and display the robot


---

### 🔹 `puzzlebot_gazebo`

This package manages the **simulation environment** of the Puzzlebot in Gazebo. It connects the robot model with the simulated world and ensures proper interaction with ROS 2.

**Main responsibilities:**
- Launch Gazebo with the custom world
- Spawn the Puzzlebot into the simulation
- Bridge communication between Gazebo and ROS 2

**Key contents:**
- `worlds/` → Custom simulation environment
- `launch/` → Gazebo and spawn launch files
- `config/` → Bridge and simulation configuration files


---

### 🔹 `puzzlebot_navigation2`

This package contains the **navigation stack configuration**, including SLAM and Nav2. It is responsible for enabling the robot to map and navigate autonomously.

**Main responsibilities:**
- Run SLAM (mapping mode)
- Configure and launch Nav2 (navigation mode)
- Manage maps and localization
- Provide visualization setups for RViz

**Key contents:**
- `config/` → YAML files for Nav2 and SLAM Toolbox
- `launch/` → Launch files for SLAM and navigation
- `maps/` → Generated or predefined maps
- `rviz/` → RViz configurations for SLAM and Nav2


---

### 🔧 Known Troubleshooting:

### 🔹 `CMake Error: The source directory does not exist.s`
If you encounter an error similar to:

```
CMake Error: The source directory "... does not exist."
```

This issue is usually caused by outdated or corrupted build cache files (`build/`, `install/`, `log/`) that still reference old or renamed directories.

#### ✅ Solution

Clean the workspace and rebuild:

```bash
rm -rf build install log
colcon build
```

This will remove cached CMake configurations and force a fresh build with the correct project structure.

#### 💡 Recommendation

After pulling new changes (especially from `develop`), it is recommended to run the clean build command above to avoid inconsistencies caused by stale cache files.
