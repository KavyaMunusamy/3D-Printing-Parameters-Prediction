# 3D Printing Parameters Prediction App

This project is a **Streamlit web application** designed to predict **optimal 3D printing parameters** for PLA material based on three mechanical properties:

* **Roughness**
* **Tension Strength**
* **Elongation**

Using machine learning (specifically, a multi-output regression model built with `LinearSVR`), the app outputs predicted printing settings such as layer height, wall thickness, infill density, infill pattern, nozzle temperature, and print speed.

---

## 📁 Project Overview

The app loads a dataset (`3d_printing_data.csv`) containing 3D printing samples. It filters the dataset for **PLA material**, encodes categorical features, scales numerical values, trains a multi-output regression model, and produces predictions based on user input.

The final model predicts the following parameters:

* Layer Height
* Wall Thickness
* Infill Density
* Infill Pattern (decoded from ordinal encoding)
* Nozzle Temperature
* Print Speed

---

## ⚙️ How the App Works

### 1. **User Inputs**

The interface takes three numerical inputs:

* Roughness
* Tension Strength
* Elongation

### 2. **Dataset Loading & Preprocessing**

* Loads `3d_printing_data.csv` using pandas.
* Filters only PLA material.
* Encodes the `infill_pattern` column using `OrdinalEncoder`.
* Drops unused columns such as `material`, `bed_temperature`, and `fan_speed`.
* Splits the data into training/testing sets.
* Scales features using `StandardScaler`.

### 3. **Model Definition**

A custom class `Model` is defined with methods:

* `fit(x, y)` — trains a multi-output regressor using `LinearSVR`.
* `predict_one_instance(x)` — scales user input, predicts the output, and inverse-transforms results.

### 4. **Model Training**

The model is trained on the processed PLA dataset.

### 5. **Prediction Output**

When the user clicks **Calculate**, the app displays predicted print settings. The encoded `infill_pattern` is transformed back to its original categorical label.

---

## 🧠 Machine Learning Model

The app uses a **MultiOutputRegressor** wrapping a **LinearSVR** model. This allows predicting multiple continuous outputs at once.

### Why LinearSVR?

* Good for small to medium numeric datasets.
* Efficient for linear relationships.
* Works well with scaled data.

### Why MultiOutputRegressor?

The printing parameters consist of **multiple independent outputs**, so a multi-output model is required.

---

## 🛠️ Technologies Used

* **Python 3**
* **Streamlit** (UI Framework)
* **Pandas** (Data handling)
* **NumPy** (Numerical operations)
* **scikit-learn** (Machine learning)

---

## ▶️ How to Run the App

1. Install dependencies:

   ```bash
   pip install streamlit pandas numpy scikit-learn
   ```

2. Place `3d_printing_data.csv` in the same directory.

3. Run the app:

   ```bash
   streamlit run app.py
   ```

4. Provide input values and press **Calculate**.

---

## 📌 Notes

* The model is trained **each time the app runs**; consider saving/loading a trained model for faster execution.
* `OrdinalEncoder` is fit on PLA-only infill patterns to decode predictions properly.
* Use proper data preprocessing when extending the dataset.

---

## 📜 License

This project can be freely used and modified.

---

## 🧩 Future Improvements

* Optimize model performance.
* Add model persistence.
* Add support for multiple materials.
* Visualize relationships between inputs and predictions.

---
