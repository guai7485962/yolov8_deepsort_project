# 🐟 使用 YOLOv4、YOLOv8 與 DeepSORT 進行魚群行為追蹤

本專案使用 **YOLOv4** 與 **YOLOv8** 進行魚群偵測，並結合 **DeepSORT** 進行多目標追蹤。專案會對魚群進行行為分析（包含平均移動距離、中心點位移、魚群密度變化）。所有模型的訓練與分析皆在 **Google Colab** 中完成，且完整的資料集已公開於 Zenodo，以確保研究的可重現性。

---

## ✅ 開始使用

我們建議在 **Google Colab** 上運行此專案。您無需進行任何額外的安裝，只需依照以下步驟操作：

### 🔹 1. 開啟 Google Colab

前往 [Google Colab](https://colab.research.google.com/) 並開啟任何一個 `.ipynb` 檔案，例如：

- `yolov8_train.ipynb`
- `distance_research.ipynb`

### 🔹 2. 下載並解壓縮資料集 (約 7.6 GB)

在第一個程式碼儲存格中執行以下指令：

```python
!wget -O yolov8_deepsort_tracking.zip "https://zenodo.org/api/records/15250169/files-archive"
!unzip yolov8_deepsort_tracking.zip -d ./project
%cd ./project/yolov8_deepsort_tracking
```

---

## 📂 資料夾結構與模組概覽

```plaintext
yolov8_deepsort_tracking/
├── data/
│   ├── object_detection_training/
│   │   ├── train/       ← 訓練圖片、標籤與過濾後圖片
│   │   ├── valid/       ← 驗證資料集
│   │   └── test/        ← 測試圖片
│   └── video/           ← 原始影片片段 (共 30 部)
│
├── training/
│   ├── yolov4/
│   │   ├── Yolov4_train_test.ipynb
│   │   └── YOLOv4 設定檔 (.cfg, .data, .names) 與訓練好的權重檔
│   └── yolov8/
│       ├── yolov8_train.ipynb
│       ├── Yolov8_test.ipynb
│       └── YOLOv8 訓練設定檔 (`fish_train_config.yaml`) 與 `best.pt`
│
├── tracking_analysis/
│   ├── distance_research.ipynb      ← 主要分析用的 Notebook
│   ├── video_data.csv               ← 包含路徑與元資料的影片清單
│   ├── deepsort_output/
│   │   ├── video/                   ← 追蹤後的影片輸出
│   │   └── txt/                     ← 追蹤數據 (bbox, ID 等)
│   └── result/
│       ├── research_output_txt/     ← 四種分析指標的逐幀輸出
│       ├── research_output_chart_img/ ← 每項分析的折線圖
│       └── summary_report.docx      ← 分析的摘要報告
```

---

## 📊 模型訓練與分析流程

### 1️⃣ YOLOv4 訓練與測試

- 📘 Notebook: `training/yolov4/Yolov4_train_test.ipynb`
- **目的**：用於和 YOLOv8 的成果進行效能比較。

---

### 2️⃣ YOLOv8 訓練與測試

- 📘 Notebook:
  - `training/yolov8/yolov8_train.ipynb`
  - `training/yolov8/Yolov8_test.ipynb`
- **輸出模型**：`best.pt`
- **目的**：提供高準確度的偵測結果，以用於 DeepSORT 追蹤階段。

---

### 3️⃣ 追蹤與魚群行為分析

- 📘 Notebook: `tracking_analysis/distance_research.ipynb`
- **輸入**：`video_data.csv` 中列出的 30 部影片
- **分析步驟**：
  1. 使用 YOLOv8 偵測魚群並透過 DeepSORT 進行追蹤。
  2. 輸出逐幀的邊界框 (bounding boxes) 與已追蹤的影片檔案。
  3. 計算以下四種行為指標：
     - `compute_avg_movement`：每幀的平均移動距離
     - `compute_center_movement`：魚群中心的位移
     - `compute_density`：魚群密度的時間變化
     - `generate_report_word`：自動生成 `.docx` 格式的摘要報告

---

## 📥 資料集來源

所有影片、訓練資料、追蹤結果與分析輸出皆可在 Zenodo 上取得。

- 📎 Zenodo 資料集連結：[🔗 https://zenodo.org/record/15250169](https://zenodo.org/record/15250169)
