# 🛰️ ISS Guardian — YOLOv8 Object Detection Microservice

**Project Overview**
ISS Guardian is a high-performance computer vision microservice built to detect critical safety equipment (fire extinguishers, toolboxes, oxygen tanks) in simulated and real-world environments. Designed for **accelerated experimentation and model building**, this system leverages an optimized YOLOv8 backbone and serves predictions via a highly decoupled REST API. It acts as a robust **data solution and pipeline for efficient ML workflows**.

---

## 🌟 Key Capabilities & Metrics

* **High-Precision Detection**: Capable of identifying objects in complex environments with high occlusion.
* **Peak Accuracy**: Achieved a final **mAP@50 of 88.6%** across all classes.
* **Microservice Architecture & REST APIs**: Lightweight Flask backend providing a programmatic JSON `/api/v1/detect` endpoint, designed for easy integration by engineering and product teams.
* **MLOps & Dockerization**: Fully containerized setup demonstrating deployment-ready data solutions and pipelines.
* **Interactive Web UI**: Built-in HTML5 frontend allowing drag-and-drop image uploads for instant inference feedback.

---

## 🚀 Model Optimization Journey

To achieve production-grade reliability, the model underwent a rigorous optimization pipeline:

1. **Baseline Validation (`yolov8s`)**: Established initial metrics, identifying raw recall as the primary bottleneck.
2. **Recall Augmentation (`yolov8m`)**: Scaled the architecture and introduced aggressive data augmentation. This drastically improved recall but temporarily elevated false positives ("hallucinations").
3. **Precision Tuning**: Implemented a custom loss configuration, elevating the `kobj` parameter to heavily penalize background false positives.
4. **Final Checkpoint**: The resulting `best.pt` strikes an optimal balance between maximizing object discovery and minimizing hallucinated bounding boxes.

---

## 🏗️ Technology Stack

* **Core ML Framework**: PyTorch, Ultralytics YOLOv8
* **Image Processing**: OpenCV, Pillow (PIL)
* **Backend API**: Python 3.10, Flask
* **Frontend**: HTML5, Tailwind CSS
* **Package Management**: Conda / Pip

---

## ⚙️ Local Setup & Inference

**1. Environment Setup**
Ensure you have Python 3.10+ installed. A CUDA-enabled GPU is recommended for training but not required for inference.

```bash
git clone <repo-url>
cd YOLOv8-ML-Microservice

# Option A: Run via Docker (Recommended for MLOps alignment)
docker-compose up --build

# Option B: Run locally
pip install -r requirements.txt
```

**2. Running the Web Application**
Start the Flask server to launch the interactive UI:
```bash
python app.py
```
*Navigate to `http://127.0.0.1:5000/` in your browser. Upload an image to see the model draw bounding boxes in real-time.*

**3. CLI Batch Inference & Verification**
To reproduce the reported metrics (mAP 88.6%) on your test set:
```bash
python predict.py --model best.pt
```

---

## 📊 Understanding Outputs

* **Web UI**: Returns a side-by-side comparison of the original image and the annotated image featuring confidence scores for `FireExtinguisher`, `ToolBox`, and `OxygenTank`.
* **CLI Engine**: Generates a comprehensive metrics table detailing `mAP50`, overall `Precision`, and `Recall`. Automatically saves a `confusion_matrix.png` to map out class-level overlaps and background misclassifications.

---

**Status:** ✅ Actively Maintained (2026)
