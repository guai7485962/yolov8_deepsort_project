# yolov8_deepsort_project
# Fish Behavior Tracking with YOLOv4, YOLOv8, and DeepSORT

本專案使用 YOLOv4 與 YOLOv8 進行魚群偵測，搭配 DeepSORT 進行多物件追蹤，最終對魚群行為（平均移動距離、中心位移、密度變化等）進行分析。所有模型訓練與分析皆於 Google Colab 完成，並已公開資料集於 Zenodo，確保研究可重現性。

---

## ✅ 如何開始

本專案建議在 **Google Colab** 上執行，無需額外安裝環境，只需依下列步驟操作：

### 🔹 1. 開啟 Google Colab
前往 [Google Colab](https://colab.research.google.com/) 並開啟任一 `.ipynb` 文件（如 `yolov8_train.ipynb` 或 `distance_research.ipynb`）。

### 🔹 2. 下載並解壓資料集（約 7.6 GB）

請於第一個 Cell 執行以下指令：

```python
!wget -O yolov8_deepsort_tracking.zip "https://zenodo.org/api/records/15250169/files-archive"
!unzip yolov8_deepsort_tracking.zip -d ./project
%cd ./project/yolov8_deepsort_tracking
