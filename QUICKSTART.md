# ⚡ Quick Start - One Page Cheat Sheet

## Installation (One-time setup)

```bash
pip install -r requirements.txt
```

**Alternative (if above fails):**
```bash
pip install flask tensorflow keras torch torchvision pennylane pennylane-qiskit qiskit numpy scipy pillow
```

---

## Step-by-Step Usage

### 1️⃣ **Prepare Dataset** (Only if you have MRI images)
```
Place your images in:
dataset/glioma/
dataset/meningioma/
dataset/notumor/
dataset/pituitary/
```

### 2️⃣ **Train Model** (30-60 minutes, requires GPU for speed)
```bash
python train.py
```
→ Saves best weights to `best_cnn_vqc.pt`

### 3️⃣ **Test with Desktop GUI** (Single image prediction)
```bash
python new_test.py
```
→ Select image file → See prediction

### 4️⃣ **Launch Web Application** (Full-featured)
```bash
python app.py
```
→ Open browser → `http://localhost:5000`
→ Register → Login → Upload image → Get prediction

---

## 📊 What Each Script Does

| Script | Purpose | Command |
|--------|---------|---------|
| `train.py` | Train model on dataset | `python train.py` |
| `new_test.py` | Test single image (GUI) | `python new_test.py` |
| `app.py` | Launch web application | `python app.py` |
| `test.py` | Legacy Keras testing UI | `python test.py` |

---

## 🔍 Expected Outputs

### Training Output:
```
Found 2500 images. Train=2000, Val=500
Epoch 1/50: Val Loss=1.2345, Val Acc=42.50%
✅ Best model saved (Acc=88.30%)
```

### Desktop Test Output:
```
Selected image: brain_tumor.jpg
Predicted: Glioma (95.32% confidence)
```

### Web App Output:
- Access at `http://localhost:5000`
- Register new account
- Login
- Upload .jpg/.png image
- See result page with prediction

---

## 🚨 Common Issues & Fixes

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| `No dataset found` | Check `dataset/` folder exists with images |
| `CUDA out of memory` | Edit `BATCH_SIZE = 8` in train.py |
| `Port 5000 already in use` | Wait 30 sec or change port in `app.py` |
| `Model not found` | Check `best_cnn_vqc.pt` exists in root folder |

---

## 📈 Project Flow

```
Start
  ↓
[1] pip install -r requirements.txt
  ↓
[2] Organize images in dataset/ folder
  ↓
[3] python train.py (optional - preloaded model available)
  ↓
[4] python new_test.py (test desktop)
  OR
[4] python app.py (test web)
  ↓
End
```

---

## 🎯 File Descriptions

- **best_cnn_vqc.pt**: Pre-trained model weights (use as-is)
- **dataset/**: Your brain tumor MRI images go here
- **app.py**: Web server (Flask)
- **train.py**: Training script
- **new_test.py**: Desktop test GUI
- **templates/**: HTML pages for web interface
- **users.db**: Auto-created user database

---

## 💻 System Requirements

- Python 3.8+
- 8GB RAM (16GB recommended)
- GPU optional (training slower on CPU)
- Internet connection (first run only, for package download)

---

## ✅ Verify Installation

```bash
# Test PyTorch
python -c "import torch; print('PyTorch OK')"

# Test PennyLane
python -c "import pennylane; print('PennyLane OK')"

# Test Flask
python -c "import flask; print('Flask OK')"
```

---

## 📝 Next Steps

After quick start:
1. Understand CNN architecture → Read `train.py` lines 50-70
2. Learn Quantum layer → Read `train.py` lines 76-90
3. Explore web features → Open `app.py`
4. Analyze predictions → Check `templates/result.html`

---

**Ready to start? Run:** `python app.py`
