# An Extended Analysis of Machine Learning Models for Maternal Health Risk Classification

## Overview

This project presents a critical re-evaluation and extension of the study  
**["Comparative Assessment of Several Effective Machine Learning Classification Methods for Maternal Health Risk"](https://cjmss.journals.ekb.eg/article_340561.html)**  
by Raihen and Akter (2024).  

While the original work compared several machine learning algorithms on the UCI Maternal Health Risk dataset, it overlooked a significant flaw: **562 duplicate records** in the dataset. Such duplicates can cause data leakage between training and test sets, inflating performance metrics and painting an overly optimistic picture of model capabilities.

Our work:

- **Replication** – Faithfully reproduce the original study’s experiments with the duplicate-containing dataset.
- **Extension** – Perform a re-analysis on a **cleaned dataset** (duplicates removed), add modern algorithms, and apply robust evaluation protocols.
- **Benchmarking** – Establish a realistic performance baseline for this task.

---

## Dataset

We use the **Maternal Health Risk Data Set** from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Maternal+Health+Risk+Data+Set), containing 1,014 samples and 7 features.

| Feature       | Description |
|---------------|-------------|
| Age           | Age in years |
| SystolicBP    | Systolic blood pressure (mmHg) |
| DiastolicBP   | Diastolic blood pressure (mmHg) |
| BS            | Blood sugar (mg/dL) |
| BodyTemp      | Body temperature (°C) |
| HeartRate     | Heart rate (bpm) |
| RiskLevel     | Target label – Low, Mid, or High risk |

**Class distribution:** Imbalanced — mid-risk class is notably smaller.

---

## Data Preprocessing

1. **Duplicates:**  
   - Found **562 duplicate records** (~55% of dataset).  
   - Removal reduced dataset to 452 unique samples.

2. **Missing Values:** None.

3. **Class Imbalance:** Addressed with **SMOTE** during training folds.

4. **Scaling:** StandardScaler applied to numerical features for scale-sensitive models.

5. **Label Encoding:** Low = 0, Mid = 1, High = 2.

6. **Outliers:** Preserved unless confirmed erroneous to keep medically relevant variations.

---

## Models Evaluated

**Original Study Models:**
- LDA – Linear Discriminant Analysis
- QDA – Quadratic Discriminant Analysis
- KNN – K-Nearest Neighbors
- Decision Tree
- Bagging
- Random Forest
- SVM – Support Vector Machine

**Additional Models:**
- MLP – Multi-layer Perceptron
- XGBoost
- CatBoost

---

## Evaluation Methodology

- **Train/Test Split:** 80/20 split, stratified.
- **10-Fold Cross-Validation:** Main evaluation method.
- **Metrics:**
  - Macro F1-Score (primary)
  - Accuracy, Precision, Recall
  - ROC-AUC per class
  - Confusion Matrix

Preprocessing steps were integrated into **pipelines** to avoid data leakage.

---

## Results

### With Duplicates (Original Dataset)

Replicating the original setup with duplicates produced high scores across models, particularly with ensembles.

| Model           | Macro F1-Score | Accuracy | Notes |
|-----------------|----------------|----------|-------|
| **Random Forest** | **0.87**       | **0.86** | Best overall, stable |
| Bagging         | 0.85           | 0.85     | Very close to RF |
| SVM             | 0.84           | 0.84     | Competitive |
| Decision Tree   | 0.83           | 0.82     | Strong and interpretable |
| KNN             | 0.82           | 0.81     | Balanced |
| XGBoost         | 0.81           | 0.81     | Strong boosting |
| CatBoost        | 0.80           | 0.80     | Similar to XGBoost |
| MLP             | 0.79           | 0.79     | Solid neural baseline |
| LDA             | 0.64           | 0.63     | Limited by linearity |
| QDA             | 0.63           | 0.65     | Bias toward high-risk class |

These values align with — and sometimes exceed — the original paper, confirming the influence of duplicate-driven leakage.

---

### Without Duplicates (Cleaned Dataset)

After removing 562 duplicates, dataset size and redundancy were reduced, making classification more challenging.  
The following represents the realistic benchmark when working with unique patient records.

| Model           | Macro F1-Score | Accuracy | Notes |
|-----------------|----------------|----------|-------|
| **SVM**         | ~0.61          | ~0.62    | Most consistent performer |
| Random Forest   | ~0.58          | ~0.59    | Remains strong |
| Bagging         | ~0.58          | ~0.59    | Matches RF closely |
| MLP             | ~0.56          | ~0.57    | Competitive neural baseline |
| XGBoost         | ~0.55          | ~0.56    | Boosting effective |
| CatBoost        | ~0.54          | ~0.55    | Similar to XGBoost |
| KNN             | ~0.53          | ~0.54    | Less stable with fewer samples |
| Decision Tree   | ~0.50          | ~0.51    | Overfits more easily now |
| LDA/QDA         | <0.50          | <0.50    | Poor low vs high risk separation |

While these numbers are lower, they reflect the true complexity of the task when evaluated on unique patient cases.  
Mid-risk classification remains strong (AUC > 0.90), but low and high-risk categories show significant feature overlap.

---

## Conclusions

- Duplicate records can substantially inflate model metrics in healthcare datasets.
- On cleaned data, **SVM** emerges as the most robust approach, though performance across all models drops when redundancy is removed.
- Mid-risk class is reliably identified; low vs high-risk separation is the main challenge.
- Achieving higher scores will likely require more diverse data and richer features.

---

## Future Work

1. **Expand dataset** – collect more samples to offset reduced size after cleaning.
2. **Advanced feature engineering** – derive new variables to enhance class separability.
3. **Explore deep learning architectures** – CNNs or Transformers for tabular healthcare data.
4. **Clinical deployment focus** – optimize inference time and model interpretability.

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.
