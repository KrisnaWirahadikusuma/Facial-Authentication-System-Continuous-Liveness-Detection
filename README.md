# Real-Time Facial Biometric Authentication and Anti-Spoofing System for Proctored Academic Examinations

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%25Vision-green.svg)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Face%25Mesh-orange.svg)](https://developers.google.com/mediapipe)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Abstract / Project Overview
Online proctoring systems are vulnerable to various forms of academic dishonesty, including presentation attacks (spoofing via static printouts or secondary display screens). This project develops a computer vision-based facial biometric verification system integrating **Continuous Liveness Detection** via Mesh Tracking algorithms. The system operates in real-time by monitoring blink mechanics and dynamically tracking subject presence to ensure academic integrity during remote evaluations.

---

## 🔬 System Architecture & Methodology

The system is engineered to minimize dependencies on heavy C++-based libraries (such as `dlib`), ensuring lightweight and reliable execution across standard hardware environments:

1. **Face Detection & Bounding Box**: 
   Leverages *MediaPipe Face Detection* to accurately isolate spatial facial coordinates in every video frame.
2. **Facial Landmark & Mesh Tessellation**: 
   Maps 468 facial landmarks using *MediaPipe Face Mesh* to render a real-time futuristic yellow tessellation grid monitoring facial geometry continuously.
3. **Active Liveness Protocol (Anti-Spoofing)**: 
   Implements vertical eyelid distance metrics (via specific landmark indices $159$ and $145$). Users are required to execute periodic blinks within a strict time threshold (`VERIFY_DURATION`) to prove biological liveness.
4. **State Machine & Auto-Reset**: 
   * If a subject exits the camera frame, the system automatically revokes verification status and triggers an acoustic alert via `winsound`.
   * If a subject re-enters, the system automatically re-initializes the scanning phase (a 4.5-second countdown) to await a fresh blink confirmation.

---

## 🛠️ Tech Stack
* **Programming Language**: Python 3.x
* **Computer Vision**: OpenCV (`cv2`)
* **Machine Learning / Feature Extraction**: Google MediaPipe Solutions
* **Utilities & Audio Feedback**: `time`, `winsound`

---

## 📂 Repository Directory Structure
```text
facial-liveness-proctoring/
│
├── main.py              # Core application logic & OpenCV interface
├── requirements.txt     # Python library dependency manifest
└── README.md            # System documentation (Academic Document)

```
⚙️ Installation & Setup Instructions
Follow these steps to configure and run the system locally:

1. Clone the Repository
Bash
git clone [https://github.com/username-kamu/nama-repo.git](https://github.com/username-kamu/nama-repo.git)
cd nama-repo
2. Configure Virtual Environment (Recommended)
Bash
python -m venv venv
# Activate virtual environment on Windows:
venv\Scripts\activate
# Activate virtual environment on macOS/Linux:
source venv/bin/activate
3. Install Dependencies
Install the required packages listed in the manifest file:

Bash
pip install -r requirements.txt
(Alternatively, install manually: pip install opencv-python mediapipe)

4. Execute the Program
Bash
python main.py
Note: Ensure your webcam is enabled. Press the ESC key on your keyboard to terminate the program.

📊 System Testing Scenarios
Testing Scenario,Input Condition,System Response / Output,Validation Status
Initial Authentication,Subject present and blinks within 4.5s,"Green bounding box, Status: Player (Verified)",Passed
Spoofing Attempt,Subject uses a static photo / phone screen,Exceeds 4.5s timeout without a fresh blink,Flagged as Cheating (Not Human!) + Alarm
Subject Absence,Subject leaves the camera field of view,Face disappears from the frame,Audio Warning + Text PERINGATAN: TIDAK ADA WAJAH!
Re-entry,Subject re-enters the frame,Automatically resets the 4.5s scanning window,Session Reset
