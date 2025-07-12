# 🚀 EfficientNetv2-L + YOLOv4 for Integrated Circuit Detection on PCBs

> 🔒 **Note**: This repository serves as a research project summary and does **not include source code or dataset** due to data confidentiality agreements. The baseline implementations referenced for this work are as follows:
>
> - **YOLOv4 original implementation**: [AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)  
> - **EfficientNetv2 official source** (Keras team): [`keras.applications.efficientnet_v2`](https://github.com/keras-team/keras/blob/6adc2bf7d8d548f92667f8337d27be6b1674ddf5/keras/src/applications/efficientnet_v2.py)  
> - **EfficientNet-YOLOv4 baseline** (Keras-based pipeline): [david8862/keras-YOLOv3-model-set](https://github.com/david8862/keras-YOLOv3-model-set)  

---

## 📘 Overview

This project was conducted as part of a master's research collaboration with Western Digital – SanDisk Storage Malaysia Sdn. Bhd. The objective was to enhance object detection performance in printed circuit board (PCB) inspection tasks, focusing specifically on the accurate localization of integrated circuit (IC) components.

By replacing the original YOLOv4 backbone with **EfficientNetv2-L** and performing systematic architecture and hyperparameter tuning, the model achieved significantly improved detection accuracy and robustness under complex visual conditions.

---

## 🎯 Objectives

- Integrate **EfficientNetv2-L** as the YOLOv4 backbone to improve feature extraction efficiency.
- Optimize anchor box settings for PCB datasets with small-scale objects.
- Experiment with various loss functions, including **CIoU** and **SIoU**.
- Evaluate the impact of **Bag of Freebies (BoF)** techniques on detection performance.

---

## 🖼️ Dataset Description

- 26,775 annotated PCB images from real manufacturing data.
- IC components vary in size, color, orientation, and texture.
- Dataset includes both original and augmented images (flipping, hue, mosaic, etc.).
- *Dataset provided under NDA and is not publicly shareable.*

---

## ⚙️ Methodology

### 🔧 Architecture Design

- **Backbone**: EfficientNetv2-L  
- **Neck**: PANet + modified FPN  
- **Head**: YOLOv4 detection layers  
- Replacement of addition with concatenation in PANet (YOLOv4 modification)

### 🧪 Training Configuration

- Image input size: 416 × 416  
- Optimizer: SGD with warm-up and cosine learning rate decay  
- Batch size: 64  
- Augmentations: Mosaic, random flip, hue shift  
- Loss functions tested: CIoU, SIoU  
- Anchor strategies: YOLOv3 default vs. dataset-specific anchors  
- BoF techniques: DropBlock, data augmentation, regularization

---

## 🧬 Experimental Settings

| Configuration       | Backbone        | Anchors        | Loss Function | BoF Applied |  
|---------------------|------------------|----------------|----------------|--------------|  
| L-ciou-y3           | EfficientNetv2-L | YOLOv3 default | CIoU           | No           |  
| L-ciou-pcban        | EfficientNetv2-L | PCB-optimized  | CIoU           | No           |  
| L-siou-pcban        | EfficientNetv2-L | PCB-optimized  | SIoU           | No           |  
| L-ciou-y3-BoF       | EfficientNetv2-L | YOLOv3 default | CIoU           | Yes          |  

---

## 📊 Results Summary

| Configuration       | F1-Score (%) | mAP (%) | Comment                            |  
|---------------------|--------------|---------|-------------------------------------|  
| L-ciou-y3           | 98.19        | 97.51   | Baseline performance                |  
| L-ciou-pcban        | 98.23        | 97.55   | Improved anchor setting             |  
| L-siou-pcban        | 98.30        | 97.72   | Best anchor + loss combo            |  
| **L-ciou-y3-BoF**   | **99.22**    | ~       | **Best overall with BoF techniques**|

---

## 🧠 Key Takeaways

- EfficientNetv2-L significantly improves performance over YOLOv4's default backbone in PCB inspection tasks.
- Customized anchor boxes tailored to IC size distributions enhance localization accuracy.
- SIoU loss function shows superior performance in this domain.
- BoF techniques can further boost detection effectiveness without increasing model size.

---

## 🔭 Future Work

- Real-time deployment on edge devices (e.g., Jetson Nano, Raspberry Pi with Coral TPU)
- Comparison with Transformer-based backbones (e.g., ConvNeXt, Swin)
- Expansion to multi-class PCB component detection tasks

---

## ✍️ Citation

If you're interested in the full research paper, you can refer to:

> Tay, S. C., et al. (2024). *Enhancing EfficientNet-YOLOv4 for Integrated Circuit Detection on Printed Circuit Boards (PCBs)*. IEEE Access, 12, 25066–25078.

---

## 📬 Contact

Feel free to reach out if you have questions or would like to collaborate.

**Tay Shiek Chi**  
📧 taysc96@gmail.com  
🌐 [LinkedIn](https://www.linkedin.com/in/s-chi-tay-859b69307/)  
