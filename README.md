# Pedestrian Protection System

This repository contains the code for a Pedestrian Protection System developed within the CARLA simulation environment. The system uses computer vision to detect pedestrians in front of a simulated vehicle and takes timely safety interventions based on a dynamic Time-to-Collision (TTC) metric. It integrates an RGB camera and a Depth camera to obtain real-time visual and distance data, processes the images using a YOLOv8n model, and controls the vehicle accordingly. Warning messages are published over MQTT for real-time monitoring.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Overview

The Pedestrian Protection System is designed to enhance safety by detecting pedestrians and taking appropriate actions to avoid collisions. It runs in the CARLA simulator and uses:
- An **RGB camera** to capture visual frames,
- A **Depth camera** to compute distances, and
- A **YOLOv8n** model for real-time pedestrian detection.

Based on the detection results, the system calculates the Time-to-Collision (TTC) and:
- Applies **soft braking** if the TTC is between 1.0 and 2.0 seconds,
- Engages **emergency braking** if the TTC is below 1.0 second (with forward control disabled and only reverse motion permitted).

The system also publishes warning messages via MQTT for real-time monitoring and logs key performance metrics for subsequent analysis.

## Prerequisites

- **CARLA Simulator:**  
  Install and launch the CARLA simulator (version 0.9.x is recommended). The simulator should be accessible on `localhost` at port `2000`.

- **Python 3.7 or Later:**  
  Ensure that Python 3.7.x is installed on your system.

- **Dependencies:**  
  The system requires the following Python packages:
  - `carla` – for simulation control and environment access
  - `pygame` – for handling user input and creating display windows
  - `opencv-python` (cv2) – for image processing and display
  - `paho-mqtt` – for MQTT messaging and communication
  - `numpy` – for numerical operations and array manipulations
  - `ultralytics` – providing the YOLOv8 model for object detection
  - `tkinter` – typically bundled with Python, used to obtain screen dimensions

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/benedettapacilli/pedestrian-protection-system.git
   cd pedestrian-protection-system
   ```

2. **Install Dependencies**

3. **Download Model Weights:**

   Download the YOLOv8n model weights from [Ultralytics' repository](https://github.com/ultralytics/assets/releases/download/v8.1.0/yolov8n.pt) and place them in the repository directory.

## Usage

1. **Launch CARLA Simulator:**

   Start the CARLA simulator (e.g., run `CarlaUE4.exe` on Windows or the equivalent command on Linux), ensuring it is running on `localhost` at port `2000`.

2. **Run the Notebook:**

   Open the provided Jupyter Notebook and run the cells sequentially. The notebook will:
   - Set up the simulation environment in CARLA.
   - Spawn a vehicle and multiple pedestrians.
   - Mount the RGB and Depth cameras on the vehicle.
   - Execute the pedestrian detection pipeline using the YOLOv8n model.
   - Log performance data (including detection distances, confidence, and TTC-based interventions) into a CSV file.
   - Publish warning messages over MQTT based on the detection results.
   - Display a real-time camera feed with bounding boxes drawn around detected pedestrians.

3. **Control the Vehicle:**

   You can manually control the vehicle using either the keyboard (via Pygame key events) or a connected joystick/steering wheel. The system will override the control in emergency scenarios based on the TTC.

## License

This project is licensed under the GPL-3.0 License.
