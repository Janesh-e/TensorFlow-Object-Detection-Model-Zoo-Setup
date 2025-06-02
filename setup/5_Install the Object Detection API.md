
# Install & Test the Object Detection API

After compiling the `.proto` files and installing the COCO API, you must install the `research/` directory as a **local Python package**. This makes `object_detection` and related modules importable in your scripts and notebooks.

> Make sure you're inside the `models/research/` folder.

```bash
cd models/research
```

You **must first copy the `setup.py` file** from the `object_detection/packages/tf2/` directory into the root of `models/research/`.

Otherwise, pip won’t know how to install the module, and you’ll get errors like `error: file setup.py not found`.

```cmd
copy object_detection\packages\tf2\setup.py .
# For Windows Command Prompt
```

(or) 

```bash
cp object_detection/packages/tf2/setup.py .
# For WSL/Linux/MacOS
```

Now run the following command:

```bash
pip install . --no-deps
```

> 🔒 The `--no-deps` flag prevents pip from modifying other installed packages (like TensorFlow & Protobuf).

After installation, run Python and check this import:

```powershell
python
>>> from object_detection.utils import config_util
>>> print(config_util)
```

(or)

```powershell
python -c "from object_detection.utils import config_util; print(config_util)"
```

If it prints a valid reference to the module (not an `ImportError`), then the installation was successful. ✅

---

### 🛠 If You Face Issues

##### Problem: `ModuleNotFoundError: No module named 'object_detection'`

- Make sure you're inside the `models/research/` folder **when running the pip install command**
- Check that `.proto` files were compiled (you should see multiple `*_pb2.py` files inside `object_detection/protos/`)
- Try uninstalling and reinstalling:

```bash
pip uninstall object-detection -y
pip install . --no-deps
```


---

## Test your Installation

Once you've successfully built and installed the TensorFlow Object Detection API using:

```bash
pip install . --no-deps
```

You should **verify that the installation works correctly** by running the official unit test provided in the `object_detection` module.

---

#### **Test the Object Detection API Installation**

> 📝 **Run this from the `models/research` directory**:

```bash
python object_detection/builders/model_builder_tf2_test.py
```

---

#### ✅ Expected Output

If everything is set up correctly, you should see output ending with:

```
[       OK ] ModelBuilderTF2Test.test_invalid_second_stage_batch_size
[ RUN      ] ModelBuilderTF2Test.test_session
[  SKIPPED ] ModelBuilderTF2Test.test_session
[ RUN      ] ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor
INFO:tensorflow:time(__main__.ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor): 0.01s
I0602 12:59:46.339357  1984 test_util.py:2460] time(__main__.ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor): 0.01s
[       OK ] ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor
[ RUN      ] ModelBuilderTF2Test.test_unknown_meta_architecture
INFO:tensorflow:time(__main__.ModelBuilderTF2Test.test_unknown_meta_architecture): 0.0s
I0602 12:59:46.339357  1984 test_util.py:2460] time(__main__.ModelBuilderTF2Test.test_unknown_meta_architecture): 0.0s
[       OK ] ModelBuilderTF2Test.test_unknown_meta_architecture
[ RUN      ] ModelBuilderTF2Test.test_unknown_ssd_feature_extractor
INFO:tensorflow:time(__main__.ModelBuilderTF2Test.test_unknown_ssd_feature_extractor): 0.0s
I0602 12:59:46.350574  1984 test_util.py:2460] time(__main__.ModelBuilderTF2Test.test_unknown_ssd_feature_extractor): 0.0s
[       OK ] ModelBuilderTF2Test.test_unknown_ssd_feature_extractor

----------------------------------------------------------------------
Ran 24 tests in 113.310s

OK (skipped=1)
```

> Note : The number of tests may vary. If it shows `OK` , you're ready to use the Object Detection API using pretrained models.

---

### ❌ Common Errors to Watch For:

- **ImportError for `tensorflow`**: Means TensorFlow isn’t installed or is incompatible.
- **`ImportError: No module named pycocotools`**: You need to install the COCO API (see previous message).
- **`ModuleNotFoundError: No module named 'object_detection'`**: This usually means the `pip install . --no-deps` step was skipped or failed.

---
