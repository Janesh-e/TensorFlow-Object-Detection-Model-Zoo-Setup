
# 📋 Prerequisites

Before beginning the TensorFlow Object Detection API setup, make sure your system meets the following basic requirements. These steps ensure you have the correct Python environment, GPU support (optional), and necessary tools to proceed smoothly.

---

## 🖥️ System Requirements

- OS: Windows 10/11 (64-bit) or Ubuntu 20.04/22.04 (Tested)
- RAM: 8 GB minimum (16 GB recommended)
- Disk Space: At least 5–10 GB free
- GPU (Optional but recommended): NVIDIA GPU with CUDA support

---

## 🔧 Tools Required

| Tool                   | Version / Note                          |
| ---------------------- | --------------------------------------- |
| Python                 | 3.8 or 3.9 (tested: 3.9.x)              |
| TensorFlow             | 2.10.1                                  |
| pip                    | Updated (≥ 20.3)                        |
| Git                    | Installed                               |
| Conda                  | Anaconda or Miniconda (not tested)      |
| Visual C++ Build Tools | Required for compilation (Windows only) |


---

### ✅ Recommended Way to Clone and Set Up

You **can clone it anywhere**, but for **cleanliness and easier navigation**, it’s recommended to:

- Create a dedicated project folder.
- Clone the repo inside it.
- Set up your Conda environment from that folder.

---

### ✅ Step-by-Step Setup (for Python 3.10 Conda environment)

#### **🐍 Step 1: Create and Activate Conda Environment**

We strongly recommend using a virtual environment to avoid package conflicts:

```powershell
conda create -n tfmodels python=3.9
conda activate tfmodels
```

---

#### **Step 2: Install TensorFlow (with GPU if desired)**

```powershell
pip install tensorflow==2.10.1  # or any compatible version for 3.10
```

---

#### **📦 Step 3: Clone the Repo into a Folder**

```bash
mkdir tf_projects
cd tf_projects
git clone https://github.com/tensorflow/models.git
cd models/research
```

This repository contains the official **TensorFlow Object Detection API** codebase, including pre-trained models and config files.

---

## ✅ Next Step

Once these prerequisites are in place, continue with:

👉 [2. CUDA & cuDNN Setup](2_cuda_cudnn.md)

---

