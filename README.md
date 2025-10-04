# Fish Behavior Tracking with YOLOv4, YOLOv5, YOLOv8, and DeepSORT

This project uses YOLOv4, YOLOv5, and YOLOv8 for fish detection, combined with DeepSORT for multi-object tracking. It performs behavioral analysis on fish groups (including average movement distance, center displacement, group density, etc.).

---

## ✅ Getting Started

We recommend running this project on **Google Colab**. No additional installation is required — just follow the steps below:

### 🔹 1. Open Google Colab

Go to [Google Colab](https://colab.research.google.com/) and open any of the `.ipynb` files (such as `yolov8_train.ipynb` or `distance_research.ipynb`).

### 🔹 2. Download and Extract Dataset (Approx. 7.6 GB)

Run the following commands in the first code cell:

```python
!wget -O yolov8_deepsort_tracking.zip "https://zenodo.org/api/records/15250169/files-archive"
!unzip yolov8_deepsort_tracking.zip -d ./project
%cd ./project/yolov8_deepsort_tracking
```

---

## ✅ Folder Structure and Module Overview

```bash
yolov8_deepsort_tracking/
├── data/
│   ├── object_detection_training/
│   │   ├── train/       ← Training images, labels, and filtered images
│   │   ├── valid/       ← Validation dataset
│   │   └── test/        ← Test images
│   └── video/           ← Original video clips (30 total)
│
├── training/
│   ├── yolov4/
│   │   ├── Yolov4_train_test.ipynb
│   │   └── YOLOv4 config files (.cfg, .data, .names) and trained weights
│   ├── yolov5/                ← NEW: Contains Yolov5 training files and weights
│   │   ├── Yolov5_train.ipynb
│   │   └── Yolov5_weights.pt
│   └── yolov8/
│       ├── yolov8_train.ipynb
│       ├── Yolov8_test.ipynb
│       └── YOLOv8 training config (`fish_train_config.yaml`) and `best.pt`
│
├── tracking_analysis/
│   ├── distance_research.ipynb      ← Main analysis notebook
│   ├── video_data.csv               ← List of videos with paths and metadata
│   ├── deepsort_output/
│   │   ├── video/                   ← Tracked video output
│   │   └── txt/                     ← Tracking data (bbox, ID, etc.)
│   └── result/
│       ├── research_output_txt/     ← Per-frame output of four analysis metrics
│       ├── research_output_chart_img/ ← Line charts for each analysis
│       ├── summary_report.docx      ← Summary report of analysis
│       └── traditional_indicator_research/   ← NEW: Holds traditional indicator research outputs
│           ├── output_image/        ← Contains images for Average NND, speed variance, group polarity
│           └── output_txt/          ← Contains text results for these three indicators
```

---

## 🆕 Changelog / 更新紀錄

- Added `training/yolov5/` folder, including Yolov5 training files and weight files for fish detection model training and testing.
- Added `tracking_analysis/result/traditional_indicator_research/output_image` and `output_txt` folders, storing images and text research results for three traditional indicators: Average NND, speed variance, and group polarity.

---

# 📊 Model Training and Analysis Pipeline

## 1️⃣ YOLOv4 Training and Testing

### 📘 `training/yolov4/Yolov4_train_test.ipynb`

**Purpose**: Used for performance comparison against YOLOv8 and YOLOv5 results.

---

## 2️⃣ YOLOv5 Training and Testing

### 📘 `training/yolov5/Yolov5_train.ipynb`

**Output model**: `Yolov5_weights.pt`  
**Purpose**: Provides additional detection model for comparative analysis in fish tracking and behavior research.

---

## 3️⃣ YOLOv8 Training and Testing

### 📘 `training/yolov8/yolov8_train.ipynb`  
### 📘 `training/yolov8/Yolov8_test.ipynb`

**Output model**: `best.pt`  
**Purpose**: Provides high-accuracy detection for use in the DeepSORT tracking phase.

---

## 4️⃣ Tracking and Fish Group Behavior Analysis

### 📘 `tracking_analysis/distance_research.ipynb`

**Input**: 30 videos listed in `video_data.csv`  
**Analysis steps**:

📌 Detect fish using YOLOv8/YOLOv5 and track using DeepSORT  
📌 Output per-frame bounding boxes and tracked video files  
📌 Compute the following four behavior metrics:

- `compute_avg_movement`: Average movement distance per frame  
- `compute_center_movement`: Displacement of group center  
- `compute_density`: Fish group density over time  
- `generate_report_word`: Auto-generate a summary `.docx` report
- Traditional indicators (Average NND, speed variance, group polarity) outputs are stored under `tracking_analysis/result/traditional_indicator_research/`

---

### 📥 Dataset Source

All videos, training data, tracking results, and analysis outputs are available on Zenodo.

### 📎 Zenodo Dataset Link

🔗 https://zenodo.org/record/15250169