# Brain Tumor Classification - Hybrid CNN + Quantum ML Model

## 📋 Project Overview

This is a **final year CSE project** that combines classical deep learning (CNN) with **quantum machine learning (QML)** to classify brain tumors from MRI images.

**What does it do?**
- Takes brain MRI images as input
- Extracts features using a Convolutional Neural Network (CNN)
- Processes features through a Quantum Circuit (QML layer)
- Classifies tumors into 4 categories: **Glioma**, **Meningioma**, **No Tumor**, or **Pituitary**
- Provides a web interface for easy predictions and user management

---

## 🏗️ Architecture & How It Works

### **1. Classical Feature Extractor (CNN)**
- **Input**: 128×128 MRI image
- **Layers**: 3 Convolutional blocks with batch normalization and ReLU activation
- **Output**: 128-dimensional feature vector
- **Purpose**: Extract spatial features from brain images efficiently

### **2. Quantum Layer (Variational Quantum Circuit)**
- **Input**: 128D features → reduced to 6 qubits (quantum bits)
- **Quantum Gates**: Angle embedding + Strongly entangling layers
- **Qubits**: 6 quantum wires with 2 layers of entanglement
- **Output**: 6-dimensional quantum measurement results
- **Purpose**: Leverage quantum superposition for advanced feature learning

### **3. Classical Classifier**
- **Input**: 6-dimensional quantum output
- **Layers**: Fully connected network (6 → 32 → 4 neurons)
- **Output**: Probability distribution over 4 tumor classes
- **Purpose**: Final classification decision

### **Overall Flow**
```
MRI Image (128×128)
    ↓
CNN Feature Extractor → 128D features
    ↓
Dimension Reduction → 6D (bounded to [-π, π])
    ↓
Quantum Circuit (6 qubits) → Process with quantum gates
    ↓
Classical Classifier → Output predictions
    ↓
Result (Glioma / Meningioma / No Tumor / Pituitary)
```

---

## 📂 Project Structure

```
final_year_project/
├── app.py                          # Flask web application
├── train.py                        # Model training script
├── test.py                         # TK GUI testing (Keras model)
├── new_test.py                     # PyTorch testing GUI
├── requirements.txt                # Python dependencies
├── best_cnn_vqc.pt                 # Trained model weights
├── dataset/                        # Training data folder
│   ├── glioma/                     # Glioma images
│   ├── meningioma/                 # Meningioma images
│   ├── notumor/                    # No tumor images
│   └── pituitary/                  # Pituitary tumor images
├── static/
│   └── uploads/                    # Uploaded images (web app)
├── templates/                      # HTML templates
│   ├── index.html
│   ├── register.html
│   ├── login.html
│   ├── predict.html
│   ├── result.html
│   ├── about.html
│   └── contact.html
└── users.db                        # User database (auto-created)
```

---

## 🚀 Quick Start Guide

### **Step 1: Install Requirements**

```bash
pip install -r requirements.txt
```

This installs:
- **PyTorch** & **TorchVision** (deep learning)
- **PennyLane** (quantum computing)
- **Qiskit** (quantum simulation)
- **Flask** (web framework)
- **TensorFlow** (Keras models)
- **PIL** (image processing)

### **Step 2: Prepare Dataset**

Download your brain tumor MRI dataset and organize it as follows:

```
dataset/
├── glioma/           (place glioma images here)
├── meningioma/       (place meningioma images here)
├── notumor/          (place no-tumor images here)
└── pituitary/        (place pituitary tumor images here)
```

📌 **Important**: Each class should be a separate folder with .jpg or .png images

### **Step 3: Train the Model** (Optional - if you have data)

```bash
python train.py
```

**What happens:**
- Loads images from `dataset/` folder
- Splits data into 80% training, 20% validation
- Trains CNN + Quantum model for 50 epochs
- Saves best model as `best_cnn_vqc.pt`
- Prints accuracy at each epoch

**Expected output:**
```
Found 2500 images. Train=2000, Val=500, Classes=['glioma', 'meningioma', 'notumor', 'pituitary']
Epoch 1/50: Val Loss=1.2345, Val Acc=42.50%
Epoch 2/50: Val Loss=0.8234, Val Acc=65.30%
...
✅ Best model saved (Acc=92.40%)
```

### **Step 4: Test the Model (Desktop GUI)**

```bash
python new_test.py
```

**What happens:**
- Opens a file dialog
- Select an MRI image
- Shows prediction with confidence score
- Example: "Predicted: Glioma (95.32% confidence)"

### **Step 5: Launch Web Application**

```bash
python app.py
```

**Access the website:**
- Open your browser → `http://localhost:5000`
- **Features:**
  - Register new user account
  - Login with email & password
  - Upload brain MRI image
  - Get instant AI prediction
  - View prediction result

---

## 📊 Model Configuration

| Parameter | Value | Purpose |
|-----------|-------|---------|
| Image Size | 128×128 | Input resolution |
| CNN Output Features | 128 | Feature vector dimension |
| Qubits | 6 | Quantum circuit wires |
| Quantum Layers | 2 | Entanglement depth |
| Classes | 4 | Glioma, Meningioma, No Tumor, Pituitary |
| Batch Size | 16 | Training samples per iteration |
| Learning Rate | 0.001 | Optimization step size |
| Epochs | 50 | Training iterations |

---

## 🎯 Key Files Explained

### **train.py**
- Loads brain tumor images from `dataset/` folder
- Builds CNN + Quantum hybrid model
- Trains on GPU/CPU (auto-detected)
- Saves weights when accuracy improves
- Takes ~2-4 hours depending on data size

### **app.py**
- Flask web server
- User authentication (register/login)
- Image upload & prediction interface
- SQLite database for users
- Routes: `/`, `/register`, `/login`, `/predict`, `/about`

### **new_test.py**
- Desktop GUI for testing (PyTorch)
- File dialog to select test image
- Shows prediction with confidence

### **test.py**
- Legacy TensorFlow/Keras testing GUI
- Similar to new_test.py but for Keras models

---

## 🔧 Troubleshooting

### **Issue: "Module not found" error**
```bash
# Solution: Reinstall requirements
pip install -r requirements_clean.txt
# Or use the cleaned version
pip install flask tensorflow keras torch torchvision pennylane pennylane-qiskit qiskit
```

### **Issue: GPU out of memory**
```python
# Edit train.py or app.py, change:
BATCH_SIZE = 8  # Reduce batch size
```

### **Issue: Dataset not loading**
- Ensure folder structure is correct:
  ```
  dataset/glioma/*.jpg
  dataset/meningioma/*.jpg
  dataset/notumor/*.jpg
  dataset/pituitary/*.jpg
  ```

### **Issue: Quantum simulator slow**
- PennyLane simulates quantum circuits on CPU → slower training
- For faster results, use smaller dataset or fewer epochs

---

## 📈 Expected Results

After training on 2000+ images:
- **Training Accuracy**: ~95%
- **Validation Accuracy**: ~88%
- **Web Prediction Time**: <2 seconds per image
- **Model Size**: ~50 MB

---

## 🎓 Learning Outcomes

This project teaches:
1. **Classical ML**: CNN architecture, image preprocessing
2. **Quantum ML**: Variational quantum circuits, quantum gates
3. **Full Stack**: Web development with Flask
4. **Database**: User authentication with SQLite
5. **ML Workflow**: Data loading, training, validation, deployment

---

## 💡 Tips for Beginner Students

1. **Start Small**: Use subset of data (50 images per class) for testing
2. **Understand Quantum**: Read PennyLane docs for quantum circuit basics
3. **GPU Acceleration**: Install CUDA for faster training
4. **Monitor Training**: Watch loss decrease in console output
5. **Save Checkpoints**: Model automatically saves best weights

---

## 📚 References

- [PennyLane Docs](https://pennylane.ai/)
- [PyTorch Documentation](https://pytorch.org/)
- [Flask Web Framework](https://flask.palletsprojects.com/)
- [Qiskit Quantum Computing](https://qiskit.org/)

---

## ✉️ Support

For issues or improvements:
1. Check error messages carefully
2. Verify dataset structure
3. Ensure all packages installed correctly
4. Check GPU/CPU availability with `torch.cuda.is_available()`

---

**Made with ❤️ for Final Year CSE Project**
