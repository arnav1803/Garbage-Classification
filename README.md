# Garbage-Classification
# 🗑️ Garbage Classification using CNN (Light-VGG16)

A deep learning project for multi-class garbage classification using a lightweight VGG16-style CNN architecture.  
This project compares:

- A **Baseline Model** (no augmentation)  
- A **Strong Augmentation Model** (geometric + photometric + quality augmentations)


---

## 📂 Dataset

**Source:** Kaggle – Garbage Classification Dataset  
https://www.kaggle.com/datasets/mostafaabla/garbage-classification  

The dataset contains **12 classes** with the following distribution:

| Class         | Files |
|---------------|--------|
| battery       | 945    |
| biological    | 985    |
| brown-glass   | 607    |
| cardboard     | 891    |
| clothes       | 5325   |
| green-glass   | 629    |
| metal         | 769    |
| paper         | 1050   |
| plastic       | 865    |
| shoes         | 1977   |
| trash         | 697    |
| white-glass   | 775    |

Total images: **14,515**

Data was split into:
- **70%** Training  
- **15%** Validation  
- **15%** Test  


---

## 🛠️ Preprocessing

Applied to all validation and test images:

- Resize → **256 px**
- CenterCrop → **227 px**
- Convert to Tensor
- Normalize using **ImageNet mean & std**

Purpose:
- Uniform input size  
- Stable model convergence  
- Align with pretrained CNN expectations  

---

## 🧠 Model Architecture (Light-VGG16)

A compact version of VGG16 with:

- Convolution + ReLU blocks  
- Batch Normalization  
- MaxPooling layers  
- Dense classifier head  
- Output layer for **12 classes**

The model was trained **end-to-end**, no frozen layers.

---

## ⚗️ Experiments

Two experiments were conducted.

---

### **A) Baseline Model**
- Only preprocessing (no augmentation)  
- Epochs: **10**  
- Optimizer: Adam  
- Loss: Categorical Crossentropy  

---

### **B) Strong Augmentation Model**

Applied only to training set.

#### **Geometric**
- RandomResizedCrop  
- HorizontalFlip  
- Rotation  

#### **Photometric**
- ColorJitter  

#### **Quality**
- GaussianBlur  
- RandomGrayscale  
- AdjustSharpness  

Trained with:
- Epochs: **20**
- Mixed Precision  
- Model Checkpointing (`best_aug_model.h5`)  

---

## ⚙️ Training Details

- **Optimizer:** Adam  
- **LR:** 0.0001  
- **Batch Size:** 16  
- **Loss:** Categorical Crossentropy  
- **Mixed Precision:** Enabled  
- **Checkpointing:** Best model saved based on validation accuracy  

Metrics monitored:
- Training Loss  
- Validation Loss  
- Training Accuracy  
- Validation Accuracy  

---

## 📊 Results

### 🔹 **Baseline vs Augmented Model**
- Augmented model generalizes significantly better  
- Lower validation loss  
- Higher validation & test accuracy  
- Less overfitting observed  

### 🔹 **Visualizations Included**
- Training vs Validation Loss  
- Training vs Validation Accuracy  
- Baseline vs Augmented comparison plots  
- Confusion Matrix  
- Classification Report  
- Actual vs Predicted distribution  



