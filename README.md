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
2026 KASA AI·S/W Mobility Autonomous Driving Competition · **Perception Lead** · MORAI SIM, ROS, Python

Owned the perception stack end to end, from raw LiDAR/camera input to the obstacle list the planner consumes.

- LiDAR detection with camera fusion (YOLO, CLRNet lanes), plus a prefilter stage (HD-map, static/dynamic, persistence) before planning
- Extended detection to 60 m to cover stopping distance at 60 km/h, holding runtime at 6–12 ms ([#116](https://github.com/FROZEN-6/MORAI_demo/pull/116))
- Traced barricade ID respawns to objects slipping between VLP-16 rings and reworked the tracker: **ID switches −67%** (120 → 40), moving-vehicle velocity accuracy 89% → 93% ([#107](https://github.com/FROZEN-6/MORAI_demo/pull/107))
- Built the replay and GT-scoring tools used to measure each change

### VLM-Based Drone Navigation · Industry Project
Aero Robotics Innovation (ARI) · **AI/Perception** · Isaac ROS, ROS 2 · Fall 2026

- Fusing Visual SLAM geometry with ViT/VLM semantics for context-aware drone autonomy (target: Jetson Orin NX)
- Set up the GPU, Docker, and Isaac ROS environment from bare metal; cuVSLAM running on stereo rosbags

### End-to-End Driving with PilotNet
[`seonhyung021/autonomous-car`](https://github.com/seonhyung021/autonomous-car) · Basis of the ACK 2026 paper

Camera-only RC car on Raspberry Pi that regresses steering and speed, with a state-machine layer for obstacle avoidance.

### MuMulYak · Medication Identification
[`seonhyung021/winter-team5`](https://github.com/seonhyung021/winter-team5) · Sookmyung Azure Winter School

Identifies a pill from one photo (Azure Custom Vision + OCR) and generates dosage guidance with Azure OpenAI.

### SafeStep · Location-Aware Fall Detection
[`seonhyung021/SafeStep`](https://github.com/seonhyung021/SafeStep) · Open Source Programming

Owned the ResNet18 stairs/ground classifier (**99.2%** / **92%+**) that sets fall risk by location, integrated with MediaPipe Pose.

---

## Coursework

- **Image Processing**: MFC implementations of histogram equalization/stretching, morphology, noise filtering, edge detection (Laplacian, Sobel across YCbCr/RGB/HSI), PSNR, geometric transforms, YCbCr skin-color face detection
- **Machine Learning / Pattern Recognition**: CNNs, RNNs, LSTM/GRU, attention, backpropagation, regularization, cross-validation
- **Applied ML**: scikit-learn pipelines (SVM + StandardScaler + RandomizedSearchCV), decision trees, AWS SageMaker Studio
