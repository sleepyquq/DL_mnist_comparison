# MNIST Pairwise Comparison Project 

## 📋 Project Overview
This project implements a deep learning-based MNIST digit comparison system that can determine the size relationship between two digits (left > right or left < right). The project adopts an end-to-end training approach, learning the comparison relationship directly from pixel data, and is specifically optimized for disturbances like occlusion in the test set.

## 🎯 Project Goals
- Implement an end-to-end digit comparison model with accuracy exceeding 70%
- Handle test data containing rotation, translation, noise, and occlusion
- Provide complete reproducible code and environment configuration

## 📊 Performance Achievements
- **Best Validation Accuracy**: 85.17% (significantly exceeding the 70% target)
- **Performance Improvement**: +15.17%
- **Model Stability**: Stable training process convergence with a standard deviation of only 0.0028

## 📁 Project File Structure
must_2025_ML_midProject/  
├── 📂 src/ # Source code directory  
│    ├── 📄 mlMid2.ipynb # Complete project code    
│    ├── 📄 mlMid2_colab.ipynb # Project run preview   
│    ├── 📄 mlMid2_en.ipynb # English version   
├── 📄 best_occlusion_model.pth # Backup of the best model weights during training (10MB)  
├── 📄 final_model_weights.pth # Final model weights file after training (10MB)  
├── 📄 training_history.json # Training history record (4KB)  
├── 📄 error_analysis.json # Error analysis report (1KB)  
├── 📄 pred_private.csv # Private test set prediction results (110KB) - Final submission file  
├── 📄 pred_public.csv # Public test set prediction results (28KB)  
├── 📄 project_summary.md # Project summary document (1KB)  
├── 📄 requirements.txt # Environment dependencies  
├── 📄 material.txt # Download links for initial files provided by the project  
└── 📄 README.md # Project description document (this file)  

## 🛠️ Environment Setup
Due to the author's computer AMD GPU limitations, the development and testing of this project were conducted entirely on colab.

### System Requirements
- Python 3.8+
- PyTorch 1.12.0+
- GPU support (recommended, but CPU can also run)

### Install Dependencies
bash
Use pip to install required packages
pip install -r requirements.txt
### requirements.txt Content
torch==1.12.1
torchvision==0.13.1
numpy==1.21.6
pandas==1.3.5
matplotlib==3.5.3
scikit-learn==1.0.2
seaborn==0.11.2
tqdm==4.64.0
Refer specifically to the code in cell 2 of `mlMid2.ipynb`. This code fully configures the environment. When testing this project on colab, simply run this code segment.

## 🚀 Quick Start
After configuring the environment, we can begin.

### 1. Data Preparation
Download the compressed package provided in `material.txt`. After extraction, you will get the data and scripts folders. The initial files required for the project are in these two folders.
Upload the initial files to colab. You can also configure Google Drive like the author did. If not needed, please ignore the code in cell 1.
When reproducing this project, pay attention to modifying the corresponding file paths in the source code, otherwise errors may occur.

### 2. Model Training
Note: Before training the model, data should be loaded. See cells 3-4.
Perform initial data preprocessing, build the model, and start training.
After the preceding code segments are executed sequentially, continue to execute the code in cells 5-7 in order. After executing the code in cell 7,
the main model training process begins, which may take some time depending on the hardware.
The models trained by the author in the early stages of the project were not ideal and suffered from overfitting. After loading the data and observing a subset of samples, it was determined that the main obstacle was data occlusion. To address this characteristic, data preprocessing, the model, and the training function were optimized. For details, refer to the comments in the corresponding parts of the source code.
The code in cells 5-7 that you see now is the optimized version.

### 3. Generate Predictions
Execute the code in cells 11-12. This will generate predictions for the public test set and the private test set respectively. The code segments have integrated the functionality of `scripts/check_submission.py`, ensuring the correct format of the prediction files.

### 4. Other
In summary, after configuring the corresponding file addresses, execute the entire source code sequentially to fully reproduce the entire project.

## ⚙️ Training Configuration

### Hyperparameter Settings
| Parameter | Value | Description |
|-----------|-------|-------------|
| Learning Rate | 0.001 | AdamW optimizer initial learning rate |
| Batch Size | 64 | Number of training samples per batch |
| Epochs | 80 | Number of complete training cycles |
| Dropout Rate | 0.5 | Regularization parameter to prevent overfitting |
| Weight Decay | 1e-4 | L2 regularization coefficient |

### Data Augmentation Strategy
- Random rotation (±10 degrees)
- Random translation (±10%)
- Random occlusion simulation (20% probability)
- Contrast and brightness adjustment

## 📈 Model Performance

### Accuracy Results
| Dataset | Sample Count | Accuracy | Note |
|---------|--------------|----------|------|
| Training Set | 50,000 | 82.97% | - |
| Validation Set | 10,000 | 85.17% | **Best Performance** |
| Public Test Set | 5,000 | 84.51% | Local Validation |

### Training Statistics
- **Model Size**: 10 MB (final weight file)
- **Training Time**: ~45 minutes (on Colab T4 GPU)
- **Parameter Count**: Approximately 1.3 million trainable parameters
- **Inference Speed**: Average 2.3ms/sample (GPU inference)

## 🔍 Error Analysis

The project includes detailed error analysis, focusing on:
- **Classification errors due to occlusion**: Error rate significantly increases for highly occluded samples.
- **Confidence distribution**: Average confidence of misclassified samples is 0.72.
- **Error types**: Analysis of false positive vs. false negative ratios.

Detailed error analysis can be found in the `error_analysis.json` file.

## 📊 Result Visualization

### Learning Curves
The training process shows a stable convergence trend:
- Training loss decreased from 0.6988 to 0.4436.
- Validation accuracy increased from 50.18% to 85.17%.
- No overfitting observed, good generalization ability.

### Confusion Matrix
The validation set confusion matrix shows balanced classification performance:
- Class 0 (left < right) accuracy: 84.92%
- Class 1 (left > right) accuracy: 85.42%

## 🎯 Technical Highlights

### Model Architecture Innovations
- **Multi-layer CNN Design**: 3 convolutional blocks + deep classifier.
- **Occlusion Robustness**: Specifically optimized for test set disturbances.
- **Adaptive Pooling**: Adapts to different input sizes.

### Training Strategy Optimization
- **Label Smoothing**: Reduces overfitting risk.
- **Gradient Clipping**: Ensures training stability.
- **Learning Rate Scheduling**: Adaptive learning rate adjustment.

### Regularization Techniques
- Batch Normalization
- Dropout (convolutional and fully connected layers)
- L2 Weight Decay

## 📋 Usage Instructions

### For Researchers
1. View `project_summary.md` for a complete project overview.
2. Analyze `training_history.json` to study the training process.
3. Refer to `error_analysis.json` to understand model limitations.

### For Developers
1. Use `best_occlusion_model.pth` for inference.
2. Refer to the prediction file format to generate new predictions.
3. Improve the model based on the existing code.

### For Evaluators
1. Verify the format correctness of `pred_private.csv`.
2. Use the provided validation script to check the submission file.
3. Refer to performance metrics for result evaluation.

## 🔧 Troubleshooting

### Common Issues
1. **Insufficient Memory**: Reduce batch size or use CPU mode.
2. **Dependency Conflicts**: Use a virtual environment to isolate package versions.
3. **Incorrect Data Path**: Ensure data files are placed in the correct directory.

### Getting Help
If encountering problems, please check:
- If the environment dependencies are completely installed.
- If the data file paths are correct.
- If file permissions are set appropriately.

## 📄 Related Documents

- **Project Summary**: `project_summary.md` - Complete project report.
- **Training History**: `training_history.json` - Detailed training process record.
- **Error Analysis**: `error_analysis.json` - Analysis of model error patterns.







