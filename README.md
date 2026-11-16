# Real-Time Object Speed Estimation using YOLOv8

> **Note:** This repository contains the core algorithm for a larger research initiative. For a complete overview, including the academic paper and contest application, please visit the main hub repository: **[Project VITAS](https://github.com/ksh0330/Project-VITAS)**.

---

## 🚗 Features

-   YOLOv8-based real-time object detection and tracking
-   Vehicle speed estimation using pixel displacement analysis
-   PyQt5 GUI for real-time monitoring and visualization
-   Multiple example implementations for different use cases
-   Simple configuration for video source and model parameters

## 📖 Method Overview

The core logic operates as follows:
1.  **Detection**: YOLOv8 detects vehicles in each frame of the video stream.
2.  **Tracking**: A simple centroid tracking algorithm assigns a unique ID to each detected vehicle.
3.  **Speed Calculation**: When a tracked vehicle crosses a predefined, hard-coded measurement zone (ROI), its pixel displacement over time is calculated and converted to real-world speed (km/h) using a manually calibrated distance constant.

## 📁 Repository Structure

```
Speed-Estimation-YOLOv8/
├── track_and_estimate.py    # Main speed estimation algorithm
├── requirements.txt        # Python dependencies
├── data/                  # Test videos (3 DCU videos)
└── examples/              # Example implementations
    ├── locations/         
    │   ├── cop.py         
    │   ├── dcu_refactored.py  
    │   ├── food.py        
    │   ├── hrc.py         
    │   ├── mac.py         
    │   └── medical_real.py 
    ├── angles/    
    │   ├── DCU_up.py        
    │   └── HRC_back.py    
    └── test_codes/        # Test and development codes
        ├── ict_code.py    
        ├── ict_code(0831).py 
        ├── py_test_316.py 
        ├── real_test.py   
        └── test3.py       
```

## ⚠️ Limitations & Constraints

This algorithm requires manual calibration for each specific video environment.

-   **Hard-coded Parameters**: The measurement zone (ROI), real-world distance, and video/model paths are hard-coded within the source code.
-   **Manual Calibration**: To function correctly, you must manually measure the physical distance of the ROI in your video's environment and update the script.

## 🛠️ Getting Started

### 1. Prerequisites
-   [Anaconda](https://www.anaconda.com/download) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) installed.
-   An NVIDIA GPU with CUDA is recommended for real-time performance.

### 2. Installation & Setup
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ksh0330/Speed-Estimation-YOLOv8.git
    cd Speed-Estimation-YOLOv8
    ```
2.  **Create and activate a new Conda environment:**
    It is highly recommended to create a dedicated environment to avoid package conflicts.
    ```bash
    conda create -n vitas-core-env python=3.9
    conda activate vitas-core-env
    ```
3.  **Install the required libraries:**
    ```bash
    pip install -r requirements.txt
    ```
    `requirements.txt` pins CUDA 12.1 builds of PyTorch and pulls them from the PyTorch wheel index.

### 3. Model Weights

-   `track_and_estimate.py` and most examples use the official **`yolov8s.pt`**. It is not stored in this repository; Ultralytics downloads it automatically on the first run.
-   Some scripts in `examples/test_codes/` load the custom-trained **`epoch52.pt`** from the VITAS contest entry. Download it from the [2024_Hanium_ICT_Contest releases](https://github.com/ksh0330/2024_Hanium_ICT_Contest/releases/latest) and place it next to the script you run.

### 4. Configuration (Required)

Before running, adjust these values in `track_and_estimate.py` for your video:

-   `video_source` (in the `__main__` block): input video path, default `data\DCU_30.mp4`. Use `0` for a webcam.
-   `self.areas["A"]` and `sourceA` (in `VideoMonitor.__init__`): pixel coordinates of the four corners of the measurement zone.
-   `self.T_W`, `self.T_H`: real-world width and length of the zone used for the perspective transform.
-   `distance_m` (in the speed calculation): real-world length of the zone in meters, default `30`.

## 🚀 How to Run

After activating the conda environment (`conda activate vitas-core-env`) and configuring the script, run it from your terminal:

```bash
python track_and_estimate.py
```