
# 🧠💓 **Spike-EchoVideo** 💾

**Spiking Visual Attention for Temporal Disease Classification in 4-Chamber Echocardiograms**

### **Project Overview**

**Spike-EchoVideo** is a research-driven project that translates biologically inspired neural dynamics into clinical diagnostic tools. While traditional AI often struggles with the "noisy" and "grainy" nature of ultrasound, our model uses **Spiking Visual Attention (SVA)** to mimic how the human brain filters visual information—focusing only on relevant cardiac motion and structural defects.

This repository adapts the **SVA mechanism** (originally for segmentation) into a **Video Classification** pipeline specifically for the **CardiacNet** dataset.

---

## **📺 The Dataset: AbnormCardiacEchoVideosThe project utilizes the CardiacNet-PAH and CardiacNet-ASD datasets**,
which consist of standardized Apical Four-Chamber (A4C) echocardiogram videos. Unlike standard medical image datasets, 
these focus on spatio-temporal inconsistencies—abnormalities that only become visible through the heart's motion over time.
Dataset SpecificationsTotal Cases: 750 high-resolution videos (800x600 or 1024x768).Frame Count: Each video contains >100 frames, capturing at least two full heartbeat cycles.
Disease Classes:PAH (Pulmonary Arterial Hypertension): 507 cases confirmed via Right Heart Catheterization.ASD (Atrial Septal Defect): 243 cases annotated by expert physicians.
Annotations: Pixel-level masks for the Left Ventricle (LV), Right Ventricle (RV), Left Atrium (LA), and Right Atrium (RA) are provided for key frames.
📽️ Visualizing Cardiac AbnormalitiesTo accurately classify these diseases, our model must differentiate between Structural (static) and Motion (dynamic) abnormalities.
ClassAbnormality TypeVisual SignatureReference GIFNormalBaselineBalanced chamber sizes and rhythmic contraction.
ASDStructuralA visible gap (hole) in the atrial septum allowing blood mixing.PAHMotionEnlarged Right Ventricle (RV) with irregular wall movement.Note to Student: 
You will find these videos in .nii.gz format in the Kaggle storage. Use the nibabel library to extract frames. 


---

### **Proposed Architecture: The SVA-Classifier**

The model consists of a three-stage pipeline designed to reduce computational load while increasing diagnostic sensitivity:

* **Encoder (Spatial):** A `DenseNet-169` backbone extracts high-level features from individual echo frames.
* **SVA Layer (Attention):** A binary spiking mask that filters out ultrasound artifacts and highlights the cardiac boundaries.
* **LIF Integrator (Temporal):** A **Leaky Integrate-and-Fire** neuron layer that accumulates "evidence" of disease over 100 frames. If the accumulated voltage exceeds a threshold, a classification is triggered.

---

### **Getting Started**

```bash
# Clone the repo
git clone https://github.com/[Your-Username]/Spike-EchoVideo.git

# Install dependencies
pip install torch spikingjelly opencv-python

```

---

[This video on ASD and Echo views](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3DD-jpsdtios) provides a clinical walkthrough of the Apical Four-Chamber view, which will help the student identify the exact regions (RV and Septum) where the Spiking Attention should be most active.
