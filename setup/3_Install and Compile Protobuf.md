
# 🧩 Install and Compile Protobuf 3.20.3 for TensorFlow Object Detection

---

## 📦 What is Protobuf?

Protobuf (Protocol Buffers) is used to serialize structured data — in TensorFlow's Object Detection API, it's required to **compile `.proto` files** that define model configuration structures.

---

## ⚠️ Warning: Avoid Breaking TensorFlow!

Installing or updating Protobuf the wrong way can cause `pip` to **downgrade your TensorFlow version** or uninstall it entirely.

> ❌ Avoid: `pip install protobuf`  
> ❌ Avoid: `pip install --upgrade protobuf`

---

### 🔧 Step 0: Install the `protoc` Compiler (Protocol Buffers CLI)

#### 🪟 For Windows

1. Go to [https://github.com/protocolbuffers/protobuf/releases/tag/v3.20.3](https://github.com/protocolbuffers/protobuf/releases/tag/v3.20.3)
2. Download `protoc-3.20.3-win64.zip` 
3. Extract the zip
4. Copy the `bin/protoc.exe` to a permanent folder like:

```
C:\Tools\protoc\bin
```

5. Add it to your system `Path`:
    - Open **Environment Variables**
    - Under "System Variables" → Edit `Path` → Add:
        
        ```
        C:\Tools\protoc\bin
        ```
        
6. Verify:

```bash
protoc --version
# Should print: libprotoc 3.20.3 (or similar)
```

---

#### 🐧 For Ubuntu/Debian Linux

```bash
sudo apt update
sudo apt install -y protobuf-compiler
```

Verify:

```bash
protoc --version
# libprotoc 3.20.3
```

You **cannot specify the exact version 3.20.3** in this command `sudo apt install -y protobuf-compiler` , because:

- `apt` only installs versions that are available in your OS's official repositories.
- Ubuntu's default `protobuf-compiler` package **often lags behind** the latest releases (usually 3.12.x or older).
- Version 3.20.3 is **not typically available** via `apt` unless you're on a bleeding-edge Ubuntu release **and** the repository has that version (which is rare).

#### Recommended method for Ubuntu :

If your version is **too old / new**, install from GitHub Releases:

```bash
# Example for version 21.12:
wget https://github.com/protocolbuffers/protobuf/releases/download/v3.20.3/protoc-3.20.3-linux-x86_64.zip
unzip protoc-21.12-linux-x86_64.zip -d protoc
sudo mv protoc/bin/* /usr/local/bin/
sudo mv protoc/include/* /usr/local/include/

# Give execution permissions (optional safety step)
sudo chmod +x /usr/local/bin/protoc

# Confirm version
protoc --version
# Expected output: libprotoc 3.20.3
```

---

#### 🍎 For macOS

```bash
brew install protobuf
# or for a specific version
brew install protobuf@3.20.3
```

---

#### 🧪 Test It

```bash
protoc --version
# Should print something like: libprotoc 3.20.3
```


---


### ✅ Step 1: Safely Install `protobuf==3.20.3`

> This version works perfectly with `tensorflow==2.10.1` and the Model Zoo repo without conflict.

Run this command:

```bash
pip install protobuf==3.20.3 --no-deps
````

> 🔒 `--no-deps` ensures pip **won’t uninstall or downgrade/upgrade TensorFlow or other packages**.

To verify, you can run :

```powershell
python -c "import google.protobuf; print(google.protobuf.__version__)"
#3.20.3
```

or,

```powershell
pip show protobuf
```

```powershell
Name: protobuf
Version: 3.20.3
Summary: Protocol Buffers
Home-page: https://developers.google.com/protocol-buffers/
Author:
Author-email:
License: BSD-3-Clause
Location: c:\users\ekamb\.conda\envs\tfod\lib\site-packages
Requires:
Required-by: apache-beam, google-api-core, googleapis-common-protos, kaggle, proto-plus, tensorboard, tensorflow, tensorflow-datasets, tensorflow-hub, tensorflow-intel, tensorflow-metadata
```

---

### 🛠 Step 2: Compile `.proto` Files

After cloning the TensorFlow Models repo, you need to compile its `.proto` files (these define the model configuration schemas).

#### 📁 Path to cloned repo (example)

```bash
/path/to/models/
└── research/
    └── object_detection/
    └── protos/
```

> Make sure you are inside the `models/research/` directory.

#### 🔧 Run this command:

```bash
cd models/research
protoc object_detection/protos/*.proto --python_out=.
```

This will generate Python files like `xxx_pb2.py` inside the `object_detection/protos/` folder.

> ✅ These files are required for the API to work during training and inference.

---

### ✅ Step 3: Set Up PYTHONPATH

Still inside the `models/research` directory:

```bash
# Linux/Mac
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

# Windows (PowerShell)
$env:PYTHONPATH="$env:PYTHONPATH;$(Get-Location);$(Get-Location)\slim"
```

To make it permanent, add it to your `.bashrc` (Linux) or environment variables (Windows).

---

### ✅ Step 4: Verify Compilation Worked

You should see many `*_pb2.py` files in `object_detection/protos/`.

Also try importing one in Python to confirm it works:

```python
# From the root of your repo
cd models/research
python
>>> from object_detection.protos import pipeline_pb2
>>> print(pipeline_pb2)
```

---

#### 🧹 If You Face Issues

- Make sure you're in the **correct folder** before running `protoc`
- Check `protobuf` version:
    
    ```bash
    pip show protobuf
    ```
    
    It should say: `Version: 3.20.3`
    
- If you see an error like `ModuleNotFoundError: No module named 'object_detection.protos.pipeline_pb2'` — re-run the `protoc` command and make sure the files were created.

---

## ✅ Next Step

After Installing & Compiling Protobuf, continue with:

👉 [4. COCO API installation](4_COCO API installation.md)

---

