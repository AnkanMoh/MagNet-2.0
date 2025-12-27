## Files Overview

### 1️⃣ `Global_logic.ipynb`

**Purpose:**
Defines the **core modeling logic** and training pipeline for the global LSTM.

**What happens here:**

* Loads training data across **multiple materials and frequencies**
* Applies **windowing** (sequence length–based slicing of signals)
* Performs **global normalization** to allow cross-material learning
* Defines the **Global LSTM architecture**
* Trains a **single shared model** instead of per-material models
* Implements:

  * Early stopping
  * Gradient clipping
  * Validation loss tracking

This notebook represents the **main architectural and training design** of the solution.

---

### 2️⃣ `Trainingdata.ipynb`

**Purpose:**
Handles **data preparation and sanity checks** before training.

**What happens here:**

* Verifies data consistency across materials and frequencies
* Inspects raw signal distributions and sequence shapes
* Confirms correct feature construction (input → target alignment)
* Ensures the dataset is compatible with the global training pipeline

This notebook is mainly used to **validate and understand the training data** before model training.

---

### 3️⃣ `Pretest.ipynb`

**Purpose:**
Runs **evaluation and pretest inference** using the trained global model.

**What happens here:**

* Loads the trained global LSTM weights
* Runs inference on unseen/pretest data
* Computes evaluation metrics (e.g., RMSE)
* Generates summary outputs and plots for performance analysis

This notebook demonstrates **model generalization** and is used for **pretest validation**.

---

### 4️⃣ `global_lstm_model.pt`

**Purpose:**
The **final trained global LSTM model weights**.

**Details:**

* Single model trained across all materials
* Used directly by `Pretest.ipynb` for inference
* Can be reused for further evaluation or submission generation

---

## Model Summary

* **Architecture:** Global LSTM
* **Input:** Time-windowed magnetic excitation features
* **Output:** Predicted magnetic response
* **Key idea:**
  Instead of training separate models per material or frequency, a **single shared model** is trained using global normalization and sequence learning to improve generalization.

---

## Typical Workflow

1. **Inspect & validate data** → `Trainingdata.ipynb`
2. **Train global model** → `Global_logic.ipynb`
3. **Run pretest / inference** → `Pretest.ipynb`
4. **Load trained weights** → `global_lstm_model.pt`


