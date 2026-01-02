
<h1 align="center">🚀 CalibRefine</h1>
<p align="center">
  <b>CalibRefine: Deep Learning-Based Online Automatic Targetless LiDAR–Camera Calibration with Iterative and Attention-Driven Post-Refinement</b>
</p>

<p align="center">
  <img src="https://img.shields.io/github/stars/radar-lab/Lidar_Camera_Automatic_Calibration?style=social" alt="GitHub Repo stars"/>
  <img src="https://img.shields.io/github/forks/radar-lab/Lidar_Camera_Automatic_Calibration?style=social" alt="GitHub forks"/>
  <img src="https://img.shields.io/github/last-commit/radar-lab/Lidar_Camera_Automatic_Calibration" alt="GitHub last commit"/>
  <a href="https://ieeexplore.ieee.org/document/11314647">
    <img src="https://img.shields.io/badge/IEEE-Published-blue.svg" alt="IEEE"/>
  </a>
  <a href="http://arxiv.org/abs/2502.17648">
    <img src="https://img.shields.io/badge/arXiv-2502.17648-b31b1b.svg" alt="arXiv"/>
  </a>
</p>

---

## 🧑‍🤝‍🧑 Contributors

<a href="https://github.com/radar-lab/Lidar_Camera_Automatic_Calibration/graphs/contributors">
  <img alt="Contributors" src="https://contrib.rocks/image?repo=radar-lab/Lidar_Camera_Automatic_Calibration" />
</a>


## 📧 Contact
- 🧑‍💻 **Author**: [Lei Cheng](https://github.com/leicheng5)  
- 🏫 **Lab**   : [Radar-Lab](https://github.com/radar-lab)  

---
## 🎯 I. Abstract
Accurate multi-sensor calibration is essential for deploying robust perception systems in applications such as autonomous driving and intelligent transportation. Existing LiDAR-camera calibration methods often rely on manually placed targets, preliminary parameter estimates, or intensive data preprocessing, limiting their scalability and adaptability in real-world settings. In this work, we propose a fully automatic, targetless, and online calibration framework, CalibRefine, which directly processes raw LiDAR point clouds and camera images. Our approach is divided into four stages: (1) a Common Feature Discriminator that leverages relative spatial positions, visual appearance embeddings, and semantic class cues to identify and generate reliable LiDAR-camera correspondences, (2) a coarse homography-based calibration that uses the matched feature correspondences to estimate an initial transformation between the LiDAR and camera frames, serving as the foundation for further refinement, (3) an iterative refinement to incrementally improve alignment as additional data frames become available, and (4) an attention-based refinement that addresses non-planar distortions by leveraging a Vision Transformer and cross-attention mechanisms. Extensive experiments on two urban traffic datasets demonstrate that CalibRefine achieves high-precision calibration with minimal human input, outperforming state-of-the-art targetless methods and matching or surpassing manually tuned baselines. Our results show that robust object-level feature matching, combined with iterative refinement and self-supervised attention-based refinement, enables reliable sensor alignment in complex real-world conditions without ground-truth matrices or elaborate preprocessing. 
<p align="center">
  <img src="https://github.com/radar-lab/Lidar_Camera_Automatic_Calibration/blob/main/Videos%20and%20Images/framework.png" width="90%">
</p>


## 📊 II. Results
### 1. Demo video for Intersection 1
[![Watch the video](https://img.youtube.com/vi/OgJkBQlzVV4/0.jpg)](https://www.youtube.com/watch?v=OgJkBQlzVV4)



### 2. Demo video for Intersection 2
[![Watch the video](https://img.youtube.com/vi/Q5gCdi36C8Y/0.jpg)](https://www.youtube.com/watch?v=Q5gCdi36C8Y)

### 3. Demo video for using the camera intrinsic matrix to rectify calibration
[![Watch the video](https://img.youtube.com/vi/4HCM0ObuQl4/0.jpg)](https://www.youtube.com/watch?v=4HCM0ObuQl4)

[![Watch the video](https://img.youtube.com/vi/K-TxdrPlns8/0.jpg)](https://www.youtube.com/watch?v=K-TxdrPlns8)







## 📌 III. LiDAR–Camera Online Automatic Targetless Calibration Steps

---

### 🔹 1. Common Feature Discriminator
- **`Train.py`** → train the Common Feature Discriminator model  
- **`Test.py`** → test the accuracy of the Common Feature Discriminator  

---

### 🔹 2. Coarse Homography Calibration
After training the Common Feature Discriminator, you can now use:  
```bash
python calibration/lidar_to_camera_calibration.py
````

This performs the **coarse calibration**.

---

### 🔹 3. Iterative Refinement

After obtaining the coarse calibration matrix, refine it by running:

```bash
python calibration/Online_Refine_Calibration_IT_finetune.py
```

📺 To visualize the calibration results:

```bash
python calibration/Video_Visualization.py
```

---

### 🔹 4. Attention-Based Refinement

After coarse calibration, you may keep refining the calibration matrix by performing **Attention-based Refinement** in the folder **`/Attention_refinement_model/`**:

* **`Train_finetune.py`** → train the Attention model
* **`Test_finetune.py`** → test the performance of the Attention model
* **`Adaptive_Correction.py`** → apply Attention-based Refinement

---

### 🔹 5. Intrinsic-Rectified Calibration

If you have the **camera intrinsic matrix**, you may choose to do **Intrinsic-Rectified Calibration** instead of Attention-based Refinement.

First run:

```bash
python rectify_image_bbox.py
```

This employs the intrinsic matrix to **rectify image distortion**.


Then, you can repeat the above calibration steps (**Coarse Homography Calibration** and **Iterative Refinement**), where the **`.py`** files ending with **`_rectify`** are specifically designed for this purpose.
