<div align="center">

# Seonhyung Kim

**Perception engineer in the making - I build the vision side of self-driving systems.**

B.S. in Artificial Intelligence Engineering, Sookmyung Women's University

<img src="https://img.shields.io/badge/Focus-Autonomous%20Driving%20Perception-1f6feb?style=flat-square" />
<img src="https://img.shields.io/badge/Field-Computer%20Vision%20%C2%B7%20Deep%20Learning-8957e5?style=flat-square" />

</div>

---

## About Me

I'm interested in the path from raw camera and LiDAR data all the way to a vehicle that actually moves.
My work centers on object detection, lane perception, sensor fusion, and getting all of it running as a real pipeline on ROS.

- Perception development across simulation (MORAI, CARLA) and small physical platforms
- End-to-end driving research on an RC car built around PilotNet
- Applied AI services on Microsoft Azure

Some of my current work lives in private repositories. Happy to walk through it on request.

---
![](./profile-3d-contrib/profile-night-rainbow.svg)

---
## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white)

**AI / Vision**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

**Robotics / Simulation**

![ROS](https://img.shields.io/badge/ROS1%20%2F%20ROS2-22314E?style=for-the-badge&logo=ros&logoColor=white)
![MORAI](https://img.shields.io/badge/MORAI%20SIM-0B5FFF?style=for-the-badge)
![CARLA](https://img.shields.io/badge/CARLA-FF6F00?style=for-the-badge)
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)

**Cloud**

![Microsoft Azure](https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)

**Tools**

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

---

## Projects

###  End-to-End Autonomous Driving with PilotNet

[`seonhyung021/autonomous-car`](https://github.com/seonhyung021/autonomous-car)

An RC car that learns to drive from camera input alone, extending NVIDIA's end-to-end approach into a **multi-output regression model that predicts steering angle and speed together.**

- Data collection pipeline on a Raspberry Pi platform (camera + ToF sensor), with stage-by-stage debug image logging
- Systematic learning-rate and scheduler experiments on the training pipeline
- Obstacle avoidance module built as a four-state machine (AVOID → STRAIGHT → RETURN → NORMAL) with linear interpolation blending on entry and exit

###  MuMulYak — Azure-Based Medication Identification & Guidance

[`seonhyung021/winter-team5`](https://github.com/seonhyung021/winter-team5) · Sookmyung Azure Winter School, Team 5

A service that identifies a medication from a single photo and generates plain-language guidance on how to take it.

- **Azure Custom Vision** for pill image classification, with confidence scores
- **Azure AI Vision (OCR)** as a second classification pass to raise accuracy on pill surface text
- **Azure OpenAI (GPT)** to generate descriptions, dosage instructions, and warnings in natural Korean
- **Gradio** frontend with custom CSS — card-based mobile-style UI, separate landing and function screens
- Images are used only transiently for analysis and never stored

###  SafeStep — Location-Aware Fall Detection & Emergency Response

[`seonhyung021/SafeStep`](https://github.com/seonhyung021/SafeStep) · Open Source Programming course team project · owned the **CNN location classifier**

A real-time system that detects falls and escalates differently depending on *where* the fall happened — stairs are treated as high-risk, flat ground as low-risk.

- **My module:** ResNet18 transfer learning (ImageNet weights, FC layer replaced for 2-class stair/ground classification), Adam lr=5e-4, class-weighted CrossEntropyLoss
- **99.2%** accuracy on stair classification, **92%+** on ground
- Resolved dataset issues: class imbalance, HEIC conversion, corrupted PNGs
- Integrated with teammates' MediaPipe Pose fall detection (hip–knee inversion, torso tilt angle, bounding-box aspect ratio) and a gTTS/Google STT emergency dialogue that escalates to an emergency call on no response

---

## Coursework & Interests

- **Image Processing** — MFC implementations of histogram equalization and stretching, morphological operations, noise filters, edge detection (Laplacian, Sobel across YCbCr/RGB/HSI), PSNR measurement, geometric transforms, and face detection via YCbCr skin-color segmentation
- **Machine Learning / Pattern Recognition** — CNNs, RNNs, LSTM/GRU, attention, backpropagation, regularization, cross-validation
- **Applied ML** — scikit-learn pipelines (SVM + StandardScaler + RandomizedSearchCV), decision trees, AWS SageMaker Studio

---
</div>
