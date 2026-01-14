# 📹 CCTV Employee Management System

A **real-time CCTV-based Employee Management System** using **YOLOv8** for person detection, **InsightFace** for face recognition, and posture classification to monitor employee behavior.  
It logs attendance, posture, and lazy behavior into CSV files for management tracking.

---

## 🚀 Features

### 👤 Employee Recognition
- Detects employees from CCTV streams using YOLOv8
- Face recognition via **InsightFace**
- Handles unknown faces gracefully
- Lightweight ReID using color histograms for fallback matching

### 🧍 Posture Monitoring
- Classifies employee posture as **Perfect** or **Lazy**
- Raises visual alerts if a person remains lazy for too long
- Logs posture information with timestamps

### 📊 Logging & Reporting
- Attendance and posture logged to `employee_logs.csv`
- Stores embeddings and ReID histograms for faster recognition
- Works with multiple camera streams simultaneously

### 🎥 Multi-Camera Support
- RTSP stream integration
- Multi-threaded processing for each camera
- Real-time monitoring with bounding boxes and labels

---

## 🏗 Project Structure

├── employee_management.py # Main CCTV employee monitoring script
├── employee_logs.csv # Generated logs (CSV)
├── Images/ # Folder with employee images for embeddings
├── requirements.txt # Python dependencies
├── README.md
└── .gitignore


---

## 🧩 Tech Stack

- **Object Detection:** YOLOv8 (Ultralytics)
- **Face Recognition:** InsightFace (`buffalo_l` model)
- **Inference:** ONNX Runtime (CPU or GPU)
- **Image Processing:** OpenCV, NumPy
- **Data Logging:** Pandas
- **Visualization:** Matplotlib (optional)
- **Threading:** Python `threading` for multi-camera support

---

## 📦 Installation

### 1️⃣ Clone Repository
```bash
git clone  https://github.com/Jasbeer-KA/cctv_employee_management_system.git
cd cctv_employee_management_system


2️⃣ Create Virtual Environment
python -m venv venv
source venv/bin/activate   # Linux / macOS
venv\Scripts\activate      # Windows

3️⃣ Install Dependencies
pip install -r requirements.txt


Requirements include: opencv-python, numpy, pandas, ultralytics, insightface, onnxruntime

▶️ Usage

Place employee images in the Images/ folder.

Filenames will be used as employee names.

Update CAMERA_URLS dictionary with your RTSP streams:

CAMERA_URLS = {
    "Camera1": "rtsp://username:password@camera_ip:port/stream",
    "Camera2": "rtsp://..."
}


Run the script:

python employee_management.py


Press q to quit any camera feed window.

🧠 How It Works

Load Employee Embeddings:
Extracts face embeddings from images stored in Images/.

Start RTSP Camera Streams:
Each camera runs in a separate thread for real-time processing.

Person Detection:
YOLOv8 detects people in the video feed.

Posture Classification:

Bounding box height > 300 → "Perfect"

Bounding box height ≤ 300 → "Lazy"

Face Recognition & ReID:

First tries InsightFace embeddings

Falls back to color histogram-based ReID if face is not detected

Logging:
Identity, posture, and timestamp are appended to employee_logs.csv.

Lazy Alerts:
Displays visual alert if an employee remains lazy for > 100 frames.

## 📝 CSV Logging
Timestamp	Identity	Posture
2026-01-14 10:00:00	JohnDoe	Perfect
2026-01-14 10:01:00	JaneDoe	Lazy

CSV file employee_logs.csv is automatically created and appended.

## 🧪 Tested Environment

Python 3.9+

Windows / Linux

CPU or GPU (ONNX Runtime)

RTSP-compatible CCTV cameras

## 🚀 Future Enhancements

Integrate database (SQLite/MySQL) for long-term storage

Real-time dashboards with Streamlit or Flask

Push notifications for lazy posture alerts

Multi-face recognition in group scenarios

GPU optimization for faster real-time processing
