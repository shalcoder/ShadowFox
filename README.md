
# 📘 ChestMNIST EffNet Model – README

This repository contains:

* A **Streamlit-based frontend** for running predictions using the **ChestMNIST EffNet V2 model**
* A **Jupyter Notebook** for training/fine-tuning the model, which can be executed in **Google Colab**

---

# 🚀 1. Running the Streamlit Application (Local Machine)

### ✅ **Requirements**

* **Windows 10/11**
* **Python 3.10.x only**
* Model folder:

  ```
  backend/model/saved_model/v2/
      chestmnist_effnet_v2.keras
      saved_model.pb
      variables/
  ```

---

## 🔧 **Step 1 — Create a Virtual Environment (Python 3.10)**

Inside the **frontend** folder:

```powershell
py -3.10 -m venv .venv
```

---

## 🔧 **Step 2 — Activate the Virtual Environment**

```powershell
.\.venv\Scripts\Activate.ps1
```

---

## 🔧 **Step 3 — Upgrade pip**

```powershell
python -m pip install --upgrade pip
```

---

## 🔧 **Step 4 — Install project dependencies**

Your `requirements.txt` must contain:

```txt
streamlit==1.38.0
ploty
tensorflow==2.19.0
keras==3.5.0
numpy==1.26.4
pillow==10.4.0
```

Install them:

```powershell
pip install -r requirements.txt
```

---

## 🎯 **Step 5 — Run the Streamlit App**

Inside the **frontend** folder:

```powershell
streamlit run app.py
```

---

## 🧠 How the Model Loads

Streamlit loads your **V2 model** using:

```python
model = keras.layers.TFSMLayer(
    "backend/model/saved_model/v2",
    call_endpoint="serving_default"
)
```

* This works **only for TensorFlow 2.19 + Keras 3+**
* V2 is a **TF SavedModel**, so this is the correct loading method

---

## 🩺 **Step 6 — Upload Image → Click Analyze**

You will see output like:

```
Predictions:
0 → 0.27
1 → 0.04
2 → 0.39
3 → 0.32
...
```

These are the **probabilities for the 7 ChestMNIST labels.**

---

# 🧪 2. Running the Training Notebook (`.ipynb`) in Google Colab

You also have:

```
Copy_of_train_chestmnist_effnet.ipynb
```

This is your training/finetuning code for ChestMNIST.

---

## 🚀 How to Run the Notebook in Google Colab

### 👉 Step 1 — Open Google Colab

[https://colab.research.google.com](https://colab.research.google.com)

### 👉 Step 2 — Upload the Notebook

Click: **File → Upload Notebook** → select your `.ipynb`

---

## ⚙️ Step 3 — Set Runtime to GPU

Go to:

```
Runtime → Change runtime type → GPU
```

---

## 📥 Step 4 — Install required libraries in the first cell:

```python
!pip install tensorflow==2.19.0 keras==3.5.0 numpy pillow scikit-learn matplotlib
```

---

## 📂 Step 5 — Upload your dataset

If you're training on ChestMNIST via MedMNIST:

```python
!pip install medmnist
```

Then load:

```python
from medmnist import ChestMNIST
```

If you want to upload your own dataset:

```
Files → Upload → Choose images
```

---

## 💾 Step 6 — Train the Model

Run the notebook cells in order.

At the end you’ll save:

```
chestmnist_effnet_v2.keras
saved_model.pb
variables/
```

You can download them with:

```python
from google.colab import files
files.download("chestmnist_effnet_v2.keras")
```

---

# 📦 Folder Structure 

```
image_tagger/
│
├── backend/
│   └── model/
│       └── saved_model/
│           └── v2/
│               ├── chestmnist_effnet_v2.keras
│               ├── saved_model.pb
│               └── variables/
│
└── frontend/
    ├── app.py
    ├── requirements.txt
    ├── .venv/
```

