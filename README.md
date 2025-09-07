# 🦴 Bone Fracture Detection (X-ray Images)

## 📌 Overview

This project focuses on **bone fracture detection** using deep learning and computer vision.
The dataset consisted of approximately **3,000 X-ray images** across various fracture types. During preprocessing, I identified issues with **imbalanced classes, missing annotations, and redundant labels**, which necessitated dataset cleaning and label remapping before training the YOLOv8 model.

---

## ⚙️ Dataset Preparation

* **Original Dataset:** 3,631 training, 348 validation, 169 test images
* **Annotation Source:** Roboflow + Manual corrections with `labelImg`
* **Problem:** Duplicate/imbalanced classes and missing annotations

### ✅ Steps Taken

1. **Annotation Fixing:**

   * Added missing bounding boxes manually using `labelImg`.
   * Verified all labels followed YOLO format (`class x_center y_center width height`).

2. **Class Cleaning:**

   * Removed duplicate class (`humerus fracture` had only 3 samples).
   * Unified the label structure to avoid confusion.

3. **Label Remapping:**

   * Original `data.yaml` had 7 classes:

     ```
     elbow positive
     fingers positive
     forearm fracture
     humerus fracture
     humerus
     shoulder fracture
     wrist positive
     ```
   * After cleaning, reduced to 6 valid classes:

     ```
     elbow positive
     fingers positive
     forearm fracture
     humerus
     shoulder fracture
     wrist positive
     ```

4. **Class Distribution After Cleaning:**

   ```
   Class 0: 385 instances (elbow positive)
   Class 1: 606 instances (fingers positive)
   Class 2: 373 instances (forearm fracture)
   Class 3: 362 instances (humerus)
   Class 4: 397 instances (shoulder fracture)
   Class 5: 262 instances (wrist positive)
   ```

---

## 🚀 Model Training

* Framework: [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
* Config:

  ```yaml
  nc: 6
  names: ["elbow positive", "fingers positive", "forearm fracture", "humerus", "shoulder fracture", "wrist positive"]
  ```
* Techniques used:

  * Patience for early stopping (`patience=5` helped reduce overfitting).
  * Cosine learning rate scheduling (`cos_lr=True`).
  * Data augmentation (flips, rotations, scale).

---

## 📊 Results

* Detected multiple fractures in unseen X-ray images.
* Successfully identified **forearm fracture, shoulder fracture, and finger positive** cases.
* Observed class imbalance challenges, but generalization improved after dataset cleaning.

---

## 🔮 Next Steps

* Expand dataset size (currently \~3K).
* Balance underrepresented classes (e.g., wrist positive).
* Explore 3D X-ray or CT-based approaches for better performance.

---

## 📂 Project Structure

```
├── dataset/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   ├── val/
│   │   ├── images/
│   │   └── labels/
│   └── test/
│       ├── images/
│       └── labels/
├── runs/
│   └── train/
│       └── bone_fracture_exp/
├── data.yaml
└── README.md
```

---

## 🙌 Acknowledgements

* [Roboflow](https://roboflow.com) for dataset tools
* [Ultralytics](https://github.com/ultralytics/ultralytics) for YOLOv8

