
Real-Time Facial Biometric Authentication and Anti-Spoofing System for Proctored Academic Examinations
Overview
Identity fraud and presentation attacks pose significant security challenges in remote examination environments. Standard face detection implementations often fail to differentiate between a live human subject and a static visual representation, such as a printed photograph or a digital display screen.

This project presents a computer vision framework designed to enforce continuous biometric verification during online evaluations. By integrating real-time facial landmark tracking with active liveness checking, the application continuously validates subject authenticity. The system relies on biological eye blink patterns to grant and maintain access authorization, effectively mitigating common bypass vectors without requiring specialized hardware.

Technical Approach & Mechanism
Unlike traditional authentication solutions that rely on heavy deep learning models or proprietary C++ binaries, this system uses a lightweight combination of OpenCV and MediaPipe Face Mesh pipelines.

1. Spatial Tracking & Mesh Tessellation
The system processes input frames from a standard webcam to extract spatial coordinates. It projects a high-density 468-point facial mesh onto the user's face, tracking structural movements dynamically across frames.

2. Active Liveness Detection (Anti-Spoofing)
To distinguish a live subject from a static presentation attack:

The application monitors the relative distance between upper and lower eyelid landmarks (specifically indices 159 and 145).

A valid eye blink event triggers a timestamp update, extending the authorized session window.

If no active blink is recorded within a set threshold (4.5 seconds), the system revokes authorization and flags the session.

3. Session State Management
Subject Absence: If the candidate exits the field of view, an acoustic warning is sounded, and the system prompts an immediate warning state.

Re-identification: Upon re-entry, the state machine resets the verification window, requiring the candidate to complete a fresh liveness check before access is restored.

Tech Stack & Dependencies
Core Language: Python 3.x

Computer Vision Framework: OpenCV (opencv-python)

Facial Landmark Pipeline: Google MediaPipe (mediapipe)

System & Signal Processing: time, winsound
