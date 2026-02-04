# 🚀 LunarSafe: Autonomous Lunar Landing System

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green)
![Gradio](https://img.shields.io/badge/Gradio-Interactive%20UI-yellow)
![Status](https://img.shields.io/badge/Status-Prototype%20Complete-success)

> **The Problem:** During the "7 Minutes of Terror" (descent phase), signal latency between Earth and the Moon (2.5s) makes real-time remote control impossible. Landers must identify hazards autonomously.
>
> **The Solution:** A decoupled computer vision architecture that detects hazards in <50ms while preserving high-fidelity visual feedback for mission control.
Dataset source: https://www.kaggle.com/datasets/romainpessia/artificial-lunar-rocky-landscape-dataset/data
---

## 🧠 Engineering Architecture: The "Enough Thinking" Approach

This project is not just a model; it is an engineered **Decoupled Rendering System**.
In real-time robotics, we face a trade-off between **Inference Speed** and **Visual Fidelity**. Processing 4K images is too slow for navigation, but downsampling destroys the visual details humans need.

**My Architecture solves this by splitting the pipeline:**

1.  **The "Brain" (Inference Stream):**
    * Downsamples input to `128x128px`.
    * Runs a **U-Net Semantic Segmentation** model.
    * **Latency:** <50ms (Real-time).
2.  **The "Eyes" (Visualization Stream):**
    * Maintains the original **High-Definition (4K)** optical feed.
    * Uses **Vector Upscaling (Linear Interpolation)** to map low-res predictions back to high-res coordinates.
    * **Result:** The operator sees a crisp, pixel-perfect overlay without sacrificing the robot's reaction speed.

---

## ✨ Key Features

### 1. U-Net Semantic Segmentation
Unlike object detection (YOLO) that only draws boxes, LunarSafe uses a **U-Net** architecture to perform pixel-level classification. This allows it to identify irregular shapes like crater rims and rock piles accurately.

### 2. Algorithmic Path Planning (Auto-Pilot)
The system doesn't just find rocks; it decides **where to land**.
* Uses **Euclidean Distance Transforms** to calculate the "Maximal Inscribed Circle" within the safe zones.
* Mathematically guarantees the largest possible safe radius for the lander's footprint.

### 3. Dynamic "Mission Control" Dashboard
An interactive UI built with **Gradio** that features:
* **Variable Sensitivity:** A slider to adjust the "Fuel vs. Risk" threshold (e.g., lower sensitivity for emergency landings).
* **Glass-Cockpit HUD:** A resolution-independent vector overlay that adapts to any camera feed size.

---

## 🛠️ Tech Stack

* **Core Logic:** Python
* **Deep Learning:** TensorFlow / Keras (U-Net Architecture)
* **Computer Vision:** OpenCV (Image Processing, Distance Transforms, HUD Rendering)
* **Deployment:** Gradio (Web Interface)

---

## 📸 Screenshots & Results

<img width="831" height="418" alt="image" src="https://github.com/user-attachments/assets/6bc4c457-2c97-4d18-a19c-5d545a8b4d72" />
<img width="1218" height="407" alt="image" src="https://github.com/user-attachments/assets/36c132ad-f4b5-4adb-a978-d94e8830ae6a" />

🔮 Future Improvements
Fuel Constraint Logic: Integrate a module to automatically widen acceptable landing radiuses as fuel decreases.

Shadow Compensation: Add a preprocessing layer to normalize lighting in deep craters (Shadow contrast enhancement).

👨‍💻 Author
Sulagna Dutta
https://www.linkedin.com/in/sulagna-dutta-ab5257358/
