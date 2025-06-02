
# 🛠️ Troubleshooting: Version Compatibility Issues

TensorFlow's Object Detection API is highly sensitive to version mismatches across multiple components — especially CUDA, cuDNN, Numpy, TensorFlow, Protobuf, and the COCO API. Even a slight deviation can break builds, cause runtime errors, or silently crash models during training/evaluation.

This guide addresses the most common **version-related issues** you might encounter while setting up the TensorFlow Object Detection API in 2025.

---

### 📌 Why Versions Matter

The components involved in the setup span multiple low-level and high-level dependencies, including:

- **CUDA & cuDNN**
- **TensorFlow**
- **Protobuf**
- **Python**
- **Numpy, Pillow, Matplotlib**
- **COCO API (`pycocotools`)**

A working combination of these must be maintained. Even though newer versions may be available, the object detection API may not yet be compatible with all of them.

---

### ✅ Best Practices

- Always check compatibility of:
    - TensorFlow ↔ CUDA / cuDNN
    - TensorFlow ↔ Python
    - TensorFlow ↔ Protobuf
- Never blindly upgrade system-wide libraries (especially protobuf, numpy, etc.) if a specific version is working.
- Prefer working in a **conda environment** to isolate versions cleanly.
- Avoid `pip install --upgrade` unless you know the exact impact.
- If installing a package **modifies the version of an already-installed library** (e.g., installing `protobuf` downgrades `tensorflow`), it’s better to use the `--no-deps` flag with `pip install` to **prevent automatic dependency resolution** that may break your setup. 

---

### ⚙️ Verified Working Setup (Example)

The setup documented in this repository uses the following working versions:

| Component      | Version Used             |
| -------------- | ------------------------ |
| Python         | 3.9.x                    |
| TensorFlow     | 2.10.1                   |
| CUDA Toolkit   | 11.2                     |
| cuDNN          | 8.9.7                    |
| Protobuf (pip) | 3.20.3                   |
| pycocotools    | from philferriere's repo |
| numpy          | 1.23.5                   |

👉 You can find the exact list of packages in [requirements_tfod.txt](requirements_tfod.txt), which was exported directly from the conda environment used to set up and run the model zoo.

---

