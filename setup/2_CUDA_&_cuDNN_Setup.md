
# ⚙️ CUDA 11.2 and cuDNN 8.9.7 Setup for TensorFlow Object Detection

> ✅ This guide helps you set up GPU support for TensorFlow in 2025, using:
> - **CUDA version:** 11.2
> - **cuDNN version:** 8.9.7

> 📌 Verified working with: `tensorflow==2.10.x`, `NVIDIA GPU with CUDA cores`

---

## 🚨 Why Specific Versions Matter

TensorFlow requires specific combinations of CUDA and cuDNN versions. The wrong pair can cause errors like:
- `Failed to load the native TensorFlow runtime`
- `cudart64_110.dll not found`
- GPU not being utilized at all

That’s why this guide pins:
- `CUDA 11.2`
- `cuDNN 8.9.7 for CUDA 11.x`

---

## 🧩 Step-by-Step CUDA & cuDNN Setup (Windows / Linux)

### 🔽 Step 1: Download CUDA 11.2

- Visit the official [NVIDIA CUDA Toolkit Archive](https://developer.nvidia.com/cuda-11.2.2-download-archive)
- Choose your **OS** and download:
  - **Windows:** "exe (local)" installer (You can choose Version 10 even if you're using Windows 11, as Windows supports backward compatible)
  - **Linux:** `.run` file or use `apt/yum` as per distro

> ✅ Choose **CUDA 11.2.2** — it’s stable and widely used

---

### 💽 Step 2: Install CUDA

- Run the downloaded CUDA installer
- Select **Custom Installation** and ensure:
  - `CUDA Toolkit` and `CUDA Runtime` are checked
  - `Visual Studio Integration` (Windows only) is optional

---

### 🔽 Step 3: Download cuDNN 8.9.7

> 📌 You need an **NVIDIA Developer Account** (free)

- Go to [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)
- Find:
  - **cuDNN 8.9.7**
  - **for CUDA 11.x**
- Download the **ZIP file** for your OS:
  - `cudnn-windows-x86_64-8.9.7.29_cuda11-archive.zip`
  - or `.tar.gz` for Linux

---

### 📁 Step 4: Copy cuDNN Files into CUDA Directory

> 🧠 After unzipping, you will see folders like `bin`, `include`, and `lib`.

**Windows example:**

1. Unzip the cuDNN archive.
2. Copy the following:

| cuDNN folder         | Paste into CUDA path                      |
|----------------------|-------------------------------------------|
| `cuda\bin\*`         | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2\bin` |
| `cuda\include\*`     | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2\include` |
| `cuda\lib\x64\*`     | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2\lib\x64` |

**Linux example:**

```bash
sudo cp cuda/include/cudnn*.h /usr/local/cuda-11.2/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda-11.2/lib64
sudo chmod a+r /usr/local/cuda-11.2/include/cudnn*.h /usr/local/cuda-11.2/lib64/libcudnn*
```

---

### 🔁 Step 5: Add to Environment Variables

#### Windows

Add these to your System Environment Variables:

|Variable|Value|
|---|---|
|`CUDA_HOME`|`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2`|
|Add to `Path`|`...CUDA\v11.2\bin` and `...CUDA\v11.2\libnvvp`|

#### Linux

Edit `~/.bashrc` or `~/.zshrc`:

```bash
export PATH=/usr/local/cuda-11.2/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-11.2/lib64:$LD_LIBRARY_PATH
```

Then run:

```bash
source ~/.bashrc
```

---

### ✅ Step 6: Verify Installation

Run this Python script:

```python
import tensorflow as tf
print("TensorFlow version:", tf.__version__)
print("Num GPUs Available:", len(tf.config.list_physical_devices('GPU')))
```

You should see:

```
TensorFlow version: 2.10.x
Num GPUs Available: 1
```


You can check the **CUDA** and **cuDNN** versions on your system in several ways depending on your OS and setup. Below are the most reliable methods for **Windows (with Conda)** or **Linux**.

#### ✅ 1. **Check CUDA Version**

#### ▶️ **Method A: Using `nvcc` (NVIDIA CUDA Compiler)**

In **Command Prompt / Terminal**:

```powershell
nvcc --version
```

This shows output like:

```powershell
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Sun_Feb_14_22:08:44_Pacific_Standard_Time_2021
Cuda compilation tools, release 11.2, V11.2.152
Build cuda_11.2.r11.2/compiler.29618528_0
```

> If you get `nvcc: command not found`, CUDA might not be added to your PATH or you may not have the toolkit installed.

---

#### ▶️ **Method B: From Conda Environment (if installed via pip/conda)**

```powershell
python -c "import tensorflow as tf; print(tf.sysconfig.get_build_info()['cuda_version'])"
```

This should return something like :

```powershell
64_112
```

or if using PyTorch:

```powershell
python -c "import torch; print(torch.version.cuda)"
```

---

#### ✅ 2. **Check cuDNN Version**

#### ▶️ **Method A: Check Files (Windows/Linux)**

Go to the CUDA installation directory:

- **Windows:**
    
    ```
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.x\include
    ```
    
- **Linux:**
    
    ```
    /usr/include/cudnn.h
    ```

Then check the version:

```bash
cat /usr/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
```

Expected output:

```
#define CUDNN_MAJOR 8
#define CUDNN_MINOR 9
#define CUDNN_PATCHLEVEL 7
```

So version is **cuDNN 8.9.7**

---

#### ▶️ **Method B: From TensorFlow (if installed)**

```bash
python -c "import tensorflow as tf; print(tf.sysconfig.get_build_info()['cudnn_version'])"
```

If installed correctly, this will show something like `64_8`.

---

#### ✅ Optional: Check GPU is Recognized

To verify your GPU and driver setup:

```bash
nvidia-smi
```

Output shows:

- Driver Version
- CUDA Version (runtime)
- GPU model
- Active processes

---

## ✅ Next Step

Once CUDA & cuDNN setup is completed, continue with:

👉 [3. Install and Compile Protobuf](3_Install and Compile Protobuf.md)

---
