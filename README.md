# An Extended Analysis of Machine Learning Models for Maternal Health Risk Classification



## Overview

This project provides a critical re-evaluation and extension of the research paper **"Comparative Assessment of Several Effective Machine Learning Classification Methods for Maternal Health Risk"**. The primary goal is to build a robust classifier for maternal health risk using the UCI Maternal Health Risk dataset, with a strong focus on methodological rigor and reproducibility.

Our analysis first replicates the methodology of the original paper and then extends it by addressing a critical flaw: the presence of 562 duplicate records in the dataset. By cleaning the data, expanding the suite of models tested, and employing robust evaluation metrics, this project offers a more realistic and reliable performance benchmark for this clinical application.

### Key Contributions
- **Data Integrity**: Identified and removed 562 duplicate records, a crucial data cleaning step overlooked in the original study, providing a more accurate foundation for model evaluation.
- **Model Expansion**: In addition to the seven models from the original paper (LDA, QDA, KNN, Decision Tree, Bagging, Random Forest, SVM), this analysis includes three modern algorithms: **XGBoost**, **CatBoost**, and a **Multi-layer Perceptron (MLP)**.
- **Robust Evaluation**: Employed both Train-Test Split and 10-Fold Cross-Validation, using the **Macro F1-Score** as the primary metric to provide a balanced assessment in the presence of class imbalance.
- **Reproducibility**: The code is structured into two distinct, well-documented phases, allowing for clear replication of both the original paper's results and our extended findings.

---

## Methodology

The analysis is divided into two main phases, each contained in a separate Jupyter notebook.

### Phase 1: Replication of the Original Study
(Notebook: `1_Replication_Original_Data.ipynb`)

This phase faithfully replicates the experiments from the source article using the **original dataset containing duplicate records**. The goal was to validate the findings of the original paper under its own data conditions.

### Phase 2: Extended Analysis on Cleaned Data
(Notebook: `2_Extended_Analysis_Cleaned_Data.ipynb`)

This phase introduces our primary contributions. The analysis is performed on the **cleaned dataset after removing all 562 duplicate rows**. This notebook evaluates all models from Phase 1, plus the three additional advanced models, establishing a more realistic performance benchmark.



---

## Key Findings

- **Impact of Duplicates**: The presence of duplicate data in the original study led to **artificially inflated performance metrics**. After cleaning the data, the top model's Macro F1-Score dropped from **~0.87** to **~0.61**.
- **Top Performing Model**: While Random Forest was the top performer on the original data, the **Support Vector Machine (SVM)** proved to be the most robust and effective model on the cleaned, unique dataset. This aligns with the original paper's conclusion but provides a more realistic performance score.
- **Class Separability**: A consistent challenge across all models was the difficulty in distinguishing the `low-risk` class, suggesting a fundamental limitation in the dataset's features for separating this specific category.

---

## How to Cite

<!-- If you use the code or findings from this project in your research, please cite our work. -->

<!-- **Our Paper (Placeholder):**
> M. R. Roohian and S. Shakour, "An Extended Analysis of Machine Learning Models for Maternal Health Risk Classification," *Journal/Conference Name*, vol. X, no. Y, pp. ZZZ-ZZZ, Year. **[Link to be added upon publication]** -->

**Original Article:**
> Raihen, M. N., & Akter, S. (2024). *Comparative Assessment of Several Effective Machine Learning Classification Methods for Maternal Health Risk*. Computational Journal of Mathematical and Statistical Sciences, 3(1), 161-176. [**Link to Paper**](https://cjmss.journals.ekb.eg/article_340561.html)

---

## License 

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

