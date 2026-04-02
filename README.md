# MNIST Pairwise Comparison Project

## 🎯 Project Purpose
The objective of this project is to develop an end-to-end deep learning system that determines the numerical relationship between two MNIST digits (Left > Right or Left < Right). The system is specifically engineered to maintain high accuracy and reliability when processing images corrupted by rotation, translation, noise, and significant occlusions found in the test datasets.

## 🛠️ Optimization Methods
To achieve robust performance and prevent overfitting, the following technical strategies were implemented:
*   **Architecture Evolution:** A multi-block CNN featuring three convolutional blocks for hierarchical feature extraction, coupled with a deep MLP classifier and Adaptive Pooling to handle varied input scales.
*   **Advanced Training Pipeline:**
    *   **Optimization:** AdamW optimizer with a 1e-4 weight decay for stable convergence.
    *   **Regularization:** High dropout (0.5), Batch Normalization, and Label Smoothing to enhance generalization.
    *   **Stability:** Gradient Clipping and an adaptive Learning Rate Scheduler to ensure numerical stability over 80 training epochs.
*   **Intensive Data Augmentation:** A rigorous augmentation suite including ±10° rotation, ±10% translation, and brightness/contrast adjustments to simulate real-world variability.

## 🚀 Key Breakthroughs
*   **Occlusion-Robust Training:** We introduced a **Random Occlusion Simulation** (20% probability) directly into the training pipeline. This forced the model to learn localized, discriminative features rather than relying on the complete digit structure, which was crucial for the corrupted test set.
*   **Analytical Refinement:** By leveraging a custom error analysis tool (`error_analysis.json`), we identified that errors were predominantly in high-occlusion scenarios. This insight allowed us to fine-tune the augmentation parameters to specifically target these failure modes.

## 📈 Achievement Showcase
*   **Superior Accuracy:** Achieved a peak validation accuracy of **85.17%**, far exceeding the 70% project target (+15.17% margin).
*   **Consistent Performance:** The model maintained an accuracy of **84.51%** on the public test set and demonstrated a stable training standard deviation of only 0.0028.
*   **Efficiency & Speed:**
    *   **Model Size:** Only 10.2 MB, making it highly portable for edge deployment.
    *   **Inference Latency:** Average of 2.3ms per sample on a T4 GPU.
*   **Reliability:** The final system provides stable, high-confidence predictions, with a final submission file `pred_private.csv` ready for evaluation.

---

### 📂 File Structure
- `src/mlMid2.ipynb`: Main source code and experimentation.
- `best_occlusion_model.pth`: Optimal weights for occlusion-heavy scenarios.
- `final_model_weights.pth`: Weights from the final training iteration.
- `requirements.txt`: Environment dependencies.

### 🔧 Quick Start
```bash
pip install -r requirements.txt
# Follow instructions in src/mlMid2.ipynb to train or predict
```

---
**Project Status:** ✅ Completed | **Final Accuracy:** 85.17% | **Target:** 70%
