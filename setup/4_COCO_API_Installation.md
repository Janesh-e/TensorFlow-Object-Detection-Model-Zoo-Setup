
# **COCO API Installation**

You should run this **from the `models/research` directory**.

```powershell
cd models/research
```

---

#### 🪟 **For Windows** (recommended via `make` alternative):

```powershell
pip install cython==3.1.0
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
```

This installs the COCO API Python bindings from a Windows-compatible fork of the official repo. You don’t need to compile it manually using `make`.

---

#### 🐧 **For Ubuntu / Linux / WSL:**

```bash
# From the root of the TensorFlow models repo
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI

# Install dependencies and compile
pip install cython
make

# Install into Python environment
pip install -e .
```

---

> ⚠️ **Why this is needed**:  
> The TensorFlow Object Detection API uses COCO tools to compute metrics like mAP and IoU during evaluation and training. Missing the COCO API may result in import errors like:

```
ModuleNotFoundError: No module named 'pycocotools'
```

---

## ✅ Next Step

After COCO API is installed:

👉 [5. Install the Object Detection API](5_Install the Object Detection API.md)

---

