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
├── GPU_check.py            # GPU availability checker
├── yolov8s.pt             # YOLOv8 model weights
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
    git clone [https://github.com/ksh0330/Speed-Estimation-YOLOv8.git](https://github.com/ksh0330/Speed-Estimation-YOLOv8.git)
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

### 3. Configuration (Required)

Before running, you **must** configure the parameters inside `track_and_estimate.py`:

-   `VIDEO_PATH`: Set the path to your input video file.
-   `WEIGHTS_PATH`: Set the path to the YOLOv8 model weights (`.pt` file).
-   `ROI_POINTS`: Define the pixel coordinates of your measurement zone.
-   `REAL_DISTANCE_METERS`: Enter the actual physical length of the zone in meters.

## 🚀 How to Run

After activating the conda environment (`conda activate vitas-core-env`) and configuring the script, run it from your terminal:

```bash
python track_and_estimate.py
```