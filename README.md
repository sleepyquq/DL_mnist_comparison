 MNIST Pairwise Comparison Project

  🎯 Project Objective
  The goal is to develop an end-to-end deep learning system that determines the numerical relationship between two MNIST
  digits (Left > Right or Left < Right). The system is specifically designed to maintain high accuracy even when inputs
  are corrupted by noise, rotation, or significant occlusions.

  🛠️ Optimization Methods
  To achieve robust performance and prevent overfitting, the following strategies were implemented:
   * Architecture: A multi-block CNN featuring 3 convolutional blocks followed by a deep MLP classifier and Adaptive
     Pooling to handle varied input scales.
   * Training Strategy:
       * AdamW Optimizer: Used with a weight decay of 1e-4 for stable convergence.
       * Regularization: High dropout (0.5), Batch Normalization, and Label Smoothing to enhance generalization.
       * Schedules: Learning rate scheduling and Gradient Clipping to ensure numerical stability during 80 epochs of
         training.
   * Data Augmentation: Intensive transformations including ±10° rotation, ±10% translation, and brightness/contrast
     adjustments.

  🚀 Key Breakthroughs
   * Occlusion-Robust Training: The primary challenge was the corrupted test set. We introduced a Random Occlusion
     Simulation (20% probability) during training, which forced the model to learn local features rather than relying on
     the whole digit structure.
   * Error-Centric Analysis: A dedicated post-training analysis (stored in error_analysis.json) helped identify that
     errors were concentrated in high-occlusion samples, leading to targeted refinement of the augmentation pipeline.

  📈 Performance Showcase
   * Accuracy: Achieved a peak validation accuracy of 85.17%, significantly exceeding the 70% target (+15.17%
     improvement).
   * Local Validation: Public test set accuracy reached 84.51%.
   * Efficiency:
       * Model Size: 10.2 MB (highly portable).
       * Inference Speed: ~2.3ms per sample on a T4 GPU.
   * Stability: The training process showed a remarkably low standard deviation of 0.0028 across runs.

  ---

  📂 File Structure Highlights
   - src/mlMid2.ipynb: Complete implementation and experimentation.
   - best_occlusion_model.pth: The highest-performing model weights.
   - pred_private.csv: Final predictions for the private test set.
   - requirements.txt: Environment configuration for reproducibility.

  🔧 Quick Start

   1 pip install -r requirements.txt
   2 # Run the notebook in src/ or the script for inference
   3 python src/mlmid2.py

  ---
  Project Status: ✅ Completed | Final Accuracy: 85.17% | Target: 70%
