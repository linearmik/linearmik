<div align="center">

# Seonhyung Kim

**Perception for autonomous systems: LiDAR, camera, and the code that turns them into decisions.**

B.S. in Artificial Intelligence Engineering, Sookmyung Women's University

<img src="https://img.shields.io/badge/Focus-Autonomous%20Driving%20Perception-1f6feb?style=flat-square" />
<img src="https://img.shields.io/badge/Field-LiDAR%20%C2%B7%20Sensor%20Fusion%20%C2%B7%20Computer%20Vision-8957e5?style=flat-square" />

</div>

---

## About

I work on the part of an autonomous stack that has to be right before anything else can be: detection, tracking, and filtering of what the sensors actually see.
Most of my time goes into LiDAR pipelines, camera–LiDAR fusion, and the evaluation tooling that tells me whether a change helped or just moved the failure somewhere else.

- Perception lead for **Team FROZEN**, 2026 KASA AI·S/W Mobility Autonomous Driving Competition (MORAI + ROS)
- Undergraduate first author, **ACK 2026** (KIPS Fall Conference), on scheduler and data-scale effects in end-to-end driving
- AI/Perception track on an industry project with **Aero Robotics Innovation (ARI)**: VLM-based drone navigation on Isaac ROS

Some of this work lives in private repositories. Happy to walk through it on request.

---
![](./profile-3d-contrib/profile-night-view.svg?v=2)
---

## Publication

**The Effect of Data Scale and Learning-Rate Scheduling in a Small-Scale
Autonomous-Driving Regression CNN: Offline and Closed-Loop Evaluation**
Seonhyung Kim, Youngmin Park (Sookmyung Women's University)
*ACK 2026, Korea Information Processing Society Fall Conference* · Poster, Nov 6 2026, Sejong University

- **180 training runs**: 2 independent datasets (22K, 14K frames) × 4 schedulers × multiple data scales × 5 seeds, plus closed-loop runs on a Raspberry Pi RC car
- Paired t-tests, TOST equivalence testing, Cohen's d<sub>z</sub>, and a decomposition of the data-scale effect
- Findings:
  1. Data scale dominates scheduler choice. Scaling up cut validation loss by 41.9–45.6%, while the largest gap between schedulers was 0.4–3.5%. The three conventional schedulers were statistically indistinguishable.
  2. OneCycle diverged more often as the dataset grew.
  3. Models with near-identical offline loss still split on closed-loop completion. Offline validation alone does not predict on-vehicle behavior.
- Journal extension in progress: multi-seed closed-loop replication and mechanism analysis

---

## Projects

### Autonomous Driving Perception · Team FROZEN
2026 KASA AI·S/W Mobility Autonomous Driving Competition · **Perception Lead** · MORAI SIM, ROS, Python · Aug–Oct 2026

Built and owned the perception stack from sensor input to the obstacle list the planner consumes.

- **Pipeline**: lane (CLRNet, IPM range 30 → 40 m) and obstacle (YOLO + LiDAR-to-image fusion) pipelines on a shared node → receiver → builder pattern
- **LiDAR detection**: RANSAC ground removal, 60 m front / ±25 m side / 25 m rear ROI, thin-object handling for cones and posts
- **Prefilter**: standalone stage before planning: HD-map off-road removal, static/dynamic classification with hysteresis, persistence gating, zone-specific rules
- **Fusion**: camera-guided recovery of cones and animals that LiDAR clustering misses; animal threshold set at 0.7 from 930 captures ([#90](https://github.com/FROZEN-6/MORAI_demo/pull/90))
- **Tunnel walls**: real-time wall extraction for the planner, wall-fragment removal 64% → 92% ([#96](https://github.com/FROZEN-6/MORAI_demo/pull/96))
- **60 m range** ([#116](https://github.com/FROZEN-6/MORAI_demo/pull/116)): stopping from 60 km/h takes ~55 m; detections past 40 m are gated to block road-surface ghosts, runtime held at 6–12 ms
- **Tracker** ([#107](https://github.com/FROZEN-6/MORAI_demo/pull/107)): a barricade slipping between VLP-16 rings at 18–21 m kept respawning under new IDs with phantom velocity. Reworked static-track memory, occlusion prediction, partial observations, and velocity filtering

| Metric (same recordings replayed) | Baseline | **Final** |
|---|---|---|
| Confirmed-ID switches (6 recordings) | 120 | **40** (−67%) |
| Static objects with false velocity (GT) | 22% | **16%** |
| Moving-vehicle velocity within ±2 m/s (GT) | 89% | **93%** |

Also wrote the replay and GT-scoring tools behind these numbers (`scripts/lidar_check/`), and supported localization and planning integration.

---

### VLM-Based Drone Autonomous Navigation · Industry Project
Aero Robotics Innovation (ARI) × Sookmyung SW-Centered University Program · **AI/Perception** · Fall 2026

Moving drone autonomy past reactive obstacle avoidance toward decisions grounded in spatial perception and visual context. My track fuses Visual SLAM geometry with lightweight ViT/VLM semantics.

- Provisioned the full GPU stack from bare metal: Ubuntu 22.04 dual-boot, NVIDIA driver 560 / CUDA 12.6, Docker + NVIDIA Container Toolkit with verified in-container GPU passthrough
- Built the Isaac ROS dev container (release-3.2, ROS 2 Humble) via `isaac_ros_common`
- Remote workflow: Tailscale mesh SSH from a MacBook, tmux for disconnect-safe builds, sleep targets masked for an always-on host
- Running Isaac ROS Visual SLAM (cuVSLAM) on stereo rosbags: real-time pose, mapping, and point clouds in RViz2
- Next: ViT semantic segmentation → 3D semantic map → VLM projection for spatial reasoning, then Isaac Sim

Dev: RTX 3060 12 GB workstation · Target: Jetson Orin NX (on-device, real-time). Partner materials are not included in any public repo.

---

### End-to-End Driving with PilotNet
[`seonhyung021/autonomous-car`](https://github.com/seonhyung021/autonomous-car) · Basis of the ACK 2026 paper

An RC car that drives from camera input alone. Extends NVIDIA's end-to-end approach to **multi-output regression of steering and speed**.

- Raspberry Pi data collection (camera + ToF) with stage-by-stage debug image logging
- Controlled scheduler and learning-rate studies across datasets, scales, and seeds
- Obstacle avoidance as a four-state machine (AVOID → STRAIGHT → RETURN → NORMAL) with linear blending on entry and exit

### MuMulYak · Medication Identification
[`seonhyung021/winter-team5`](https://github.com/seonhyung021/winter-team5) · Sookmyung Azure Winter School, Team 5

Identifies a pill from one photo and generates plain-language dosage guidance.

- Azure Custom Vision classification, with Azure AI Vision OCR on imprint text as a second pass
- Azure OpenAI for Korean descriptions, dosage instructions, and warnings
- Gradio frontend with a card-based mobile layout; images processed transiently, never stored

### SafeStep · Location-Aware Fall Detection
[`seonhyung021/SafeStep`](https://github.com/seonhyung021/SafeStep) · Open Source Programming · Owned the **CNN location classifier**

Detects falls and escalates by location: stairs high-risk, flat ground low-risk.

- ResNet18 transfer learning (ImageNet weights, 2-class head), Adam lr=5e-4, class-weighted cross-entropy
- **99.2%** on stairs, **92%+** on ground; cleaned class imbalance, HEIC conversion, and corrupted PNGs
- Integrated with MediaPipe Pose fall detection and a gTTS/STT dialogue that escalates to an emergency call on no response

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white)

**Perception / ML**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

**Robotics / Simulation**

![ROS](https://img.shields.io/badge/ROS1%20%2F%20ROS2-22314E?style=for-the-badge&logo=ros&logoColor=white)
![Isaac ROS](https://img.shields.io/badge/Isaac%20ROS-76B900?style=for-the-badge&logo=nvidia&logoColor=white)
![MORAI](https://img.shields.io/badge/MORAI%20SIM-0B5FFF?style=for-the-badge)
![CARLA](https://img.shields.io/badge/CARLA-FF6F00?style=for-the-badge)
![Jetson](https://img.shields.io/badge/Jetson-76B900?style=for-the-badge&logo=nvidia&logoColor=white)
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)

**Infra / Cloud**

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-76B900?style=for-the-badge&logo=nvidia&logoColor=white)
![Microsoft Azure](https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

---

## Coursework

- **Image Processing**: MFC implementations of histogram equalization/stretching, morphology, noise filtering, edge detection (Laplacian, Sobel across YCbCr/RGB/HSI), PSNR, geometric transforms, YCbCr skin-color face detection
- **Machine Learning / Pattern Recognition**: CNNs, RNNs, LSTM/GRU, attention, backpropagation, regularization, cross-validation
- **Applied ML**: scikit-learn pipelines (SVM + StandardScaler + RandomizedSearchCV), decision trees, AWS SageMaker Studio
