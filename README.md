# 🔬 Histopathology & Cell Morphology Analytics Pipeline

An end-to-end clinical data analytics and machine learning pipeline processing **569 digitized Fine Needle Aspirate (FNA) biopsy samples**. This project analyzes 30 microscopic nuclear features with standardized cytometric physical units ($\mu m$, $\mu m^2$) to classify tissue pathology into `Malignant` or `Benign` pathology grades.

---

## 📖 Data Dictionary & Cytometric Units

| Feature Group | Example Variable | Data Type | Physical Units | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Nucleus Size** | `nucleus_radius_mean_um` | Float | $\mu m$ (Micrometers) | Mean distance from nucleus center to perimeter |
| **Nucleus Area** | `nucleus_area_mean_sq_um` | Float | $\mu m^2$ (Square Micrometers) | Total cross-sectional area of the cell nucleus |
| **Texture Density** | `nucleus_texture_gray_sd` | Float | Gray-scale SD | Standard deviation of gray-scale image intensity |
| **Atypic Concavity** | `nucleus_concavity_score` | Float | Ratio Score ($0.0 - 1.0$) | Severity of cell membrane concavities/indentations |
| **Extreme Metrics** | `worst area`, `worst concave points` | Float | $\mu m^2$ / Count | Maximum extreme values recorded across biopsy cells |
| **Diagnosis Label** | `pathology_label` | Categorical | Binary Label | Clinical outcome (`Malignant` vs. `Benign`) |

---

## 🏗️ Architecture & Pipeline Flow

1. **Clinical Data Ingestion & Standardization:**
   - Ingested digitized FNA biopsy records across 30 cytometric parameters.
   - Renamed feature dimensions to reflect micrometer physical units ($\mu m$, $\mu m^2$).

2. **Exploratory Data Analysis & Morphological Boxplots:**
   - Visualized nuclear radius and membrane concavity distributions across pathology grades.
   - Confirmed cytological atypia: malignant nuclei demonstrate double the mean radius and triple the concavity score of benign cells.

3. **Machine Learning Model (`Scikit-Learn` Random Forest):**
   - Trained a 100-tree `RandomForestClassifier` on 80% stratified training data.
   - Achieved **96% overall accuracy** and an **ROC-AUC score of 0.99+** on unseen test biopsies.

4. **Production Clinical Inference Simulation:**
   - Implemented a decision-support function evaluating unseen sample payloads in real time, returning diagnostic labels with probability confidence scores.

---

## 📊 Clinical Model Performance & Visualizations

| Metric | Score | Clinical Relevance |
| :--- | :--- | :--- |
| **Accuracy** | **96.0%** | Correctly classified 109 out of 114 test biopsies |
| **Malignant Precision** | **95.0%** | Low false-positive diagnostic rate |
| **Malignant Recall** | **93.0%** | Successfully identified 39 of 42 malignant biopsy cases |
| **Benign Recall** | **97.0%** | High specificity in ruling out malignancy |

### Morphological Feature Distributions
![Morphology Boxplots](clinical_morphology_distribution.png)

### Model Confusion Matrix
![Confusion Matrix](clinical_model_evaluation.png)

### Morphological Feature Importance
![Feature Importance](clinical_feature_importance.png)

---

## 🛠️ Tech Stack & Dependencies

- **Language:** Python 3.10+
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning:** Scikit-Learn (`RandomForestClassifier`, `train_test_split`, `metrics`)
- **Visualization:** Seaborn, Matplotlib
