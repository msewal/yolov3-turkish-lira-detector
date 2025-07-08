# YOLOv3 Turkish Lira Detector

**Detect and classify Turkish Lira banknotes (5₺, 10₺, 20₺, 50₺, 100₺, 200₺) in images using YOLOv3.**

## 🚀 Features

* Six-class object detection for Turkish Lira banknotes
* Training with Darknet YOLOv3 architecture
* Step-by-step Google Colab notebooks
* GPU and OpenCV acceleration for faster training and inference

## 📂 Project Structure

```
yolov3-turkish-lira-detector/
├── Colab_Notebooks/
│   ├── DeepLearning_ED.ipynb        # Intro to deep learning concepts
│   ├── Train_YoloV3_.ipynb          # YOLOv3 training guide on Colab
│   ├── images.zip                   # Banknote images and label files
│   └── ...                          # Auto-saved notebooks
├── cfg/
│   ├── yolov3.cfg                   # Original YOLOv3 configuration
│   └── yolov3_training.cfg          # Training configuration
├── data/
│   ├── obj.names                    # Class names file (6 entries)
│   ├── obj.data                     # Data configuration file
│   ├── train.txt                    # List of training image paths
│   └── valid.txt                    # List of validation image paths
├── LICENSE                          # MIT License file
└── README.md                        # This README file
```

## ⚙️ Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/<username>/yolov3-turkish-lira-detector.git
   cd yolov3-turkish-lira-detector
   ```

2. **Open Google Colab:**

   * Upload `Colab_Notebooks/Train_YoloV3_.ipynb` to your Colab workspace.
   * Mount your Google Drive:

     ```python
     from google.colab import drive
     drive.mount('/content/drive')
     ```

3. **Build Darknet:**

   ```bash
   !git clone https://github.com/AlexeyAB/darknet.git
   %cd darknet
   !sed -i 's/GPU=0/GPU=1/' Makefile
   !sed -i 's/OPENCV=0/OPENCV=1/' Makefile
   !make
   ```

## 🎓 Training

1. **Configure training files:**

   * Copy `cfg/yolov3.cfg` to `cfg/yolov3_training.cfg`.
   * In `yolov3_training.cfg`, set `classes=6` and adjust `batch`, `subdivisions`, and other hyperparameters as needed.
   * Update paths in `data/obj.names`, `data/obj.data`, `train.txt`, and `valid.txt`.

2. **Unzip the dataset:**

   ```bash
   !unzip "../Colab_Notebooks/images.zip" -d data/obj
   ```

3. **Start training:**

   ```bash
   !./darknet detector train data/obj.data cfg/yolov3_training.cfg darknet53.conv.74
   ```

## 🔍 Inference

After training completes, run inference on a test image:

```bash
!./darknet detector test data/obj.data cfg/yolov3_training.cfg backup/yolov3_training_last.weights data/test.jpg
```

The output image with detections will be saved as `predictions.jpg`.

