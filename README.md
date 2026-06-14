# 🌸 Iris Species: The Botanist's Classifier

> **From field measurements to data-driven species identification** — a complete classification pipeline that replaces subjective visual judgment with a 3-rule protocol achieving ~96% accuracy.

---

## 📌 Project Overview

Field botanists have long relied on subjective visual cues to classify Iris species — a process that is slow, inconsistent across observers, and error-prone, particularly when distinguishing *Versicolor* from *Virginica*. This project analyzes 150 flower measurements across 4 physical dimensions to uncover quantifiable species boundaries and deliver a replicable, data-backed identification framework that any researcher can apply — no machine learning tools required in the field.

**Key outcome:** A 3-rule field protocol that reduces misclassification from ~15% (manual) to under 5% — roughly a 3× improvement.

---

## 📁 Repository Structure

```
iris-botanist-classifier/
│
├── Iris_Botanist_Classifier.ipynb   # Full analysis notebook (EDA → ML → Rulebook)
├── Iris.csv                         # Dataset — 150 observations, 4 features, 3 species
├── Iris_Botanist_Classifier.pptx    # Slide deck — 12-slide stakeholder presentation
└── README.md
```

---

## 📊 Dataset

| Property | Detail |
|---|---|
| Source | UCI Iris Dataset |
| Observations | 150 (50 per species) |
| Features | SepalLength, SepalWidth, PetalLength, PetalWidth (all in cm) |
| Target | Species: *Iris-setosa*, *Iris-versicolor*, *Iris-virginica* |
| Missing Values | None |
| Class Balance | Perfectly balanced — 33.3% each |

---

## 🔬 Analysis Pipeline

### 1. Data Loading & Cleaning
- Dropped the non-informative `Id` column
- Renamed columns for readability
- Verified zero missing values and zero duplicate records
- Applied 3-sigma outlier detection — one outlier (Row 16, SepalWidth = 4.4 cm) retained as a confirmed valid botanical measurement

### 2. Exploratory Data Analysis (EDA)
- Mean feature comparison across all three species (grouped bar chart)
- Cross-variable pair plot (4×4 scatter matrix with diagonal histograms)
- Box plots revealing variance and inter-species overlap in petal dimensions

**Key EDA finding:** Petal Length shows the largest inter-species mean difference (1.46 → 4.26 → 5.55 cm) — making it the strongest natural classifier by a significant margin.

### 3. Variance & Boundary Analysis
- Box plots confirm non-overlapping IQRs for Petal Length across all three species
- Scatter plot with decision boundary lines (PL = 2.5 cm and PL = 4.75 cm) visually validates the threshold-based rules

### 4. Machine Learning Classification

Four models were trained and evaluated using 5-fold cross-validation on an 80/20 train-test split:

| Model | CV Accuracy |
|---|---|
| Random Forest (Model A) | ~96–97% |
| Logistic Regression (Model B) | ~96% |
| K-Nearest Neighbors (Model C) | ~96% |
| Support Vector Machine (Model D) | ~97% |

All models comfortably exceeded 96% cross-validated accuracy. Random Forest was selected as the best model for detailed evaluation.

**Confusion matrix result:** Setosa classified with 100% accuracy. Only 3 misclassifications — all in the Versicolor/Virginica overlap zone, consistent with visual analysis findings.

### 5. Feature Importance (Random Forest)
- Petal dimensions combined account for ~86% of classification power
- Sepal Width was the least useful standalone feature

### 6. Species Identification Rulebook

The core deliverable — a 3-rule field protocol requiring no digital tools:

```
Rule 1:  Petal Length < 2.5 cm          →  Iris SETOSA
         (confirm: Petal Width < 0.6 cm)

Rule 2:  Petal Length between 2.5–4.75 cm  →  Iris VERSICOLOR
         (confirm: Petal Width 1.0–1.8 cm)

Rule 3:  Petal Length > 4.75 cm         →  Iris VIRGINICA
         (confirm: Petal Width > 1.8 cm)

Edge case:  If Petal Length ≈ 4.5–5.0 cm,
            verify Sepal Length > 6.0 cm to confirm Virginica.
```

**Rulebook accuracy on full dataset: ~96%**

| Species | Rulebook Accuracy |
|---|---|
| Setosa | 100% |
| Versicolor | ~94% |
| Virginica | ~94% |

---

## 🔑 Key Findings

1. **Petal dimensions drive classification** — Petal Length + Petal Width account for ~86% of model classification power
2. **Setosa is fully separable** — zero overlap with the other two species across all features
3. **Three thresholds are enough** — the rulebook classifies ~96% of specimens correctly without any software
4. **All ML models exceeded 96% accuracy** — validating that the underlying data structure is highly learnable
5. **Field improvement:** ~15% manual error rate → under 5% with the rulebook (~3× more accurate)

---

## 🛠️ Tech Stack

- **Python 3.x**
- `pandas`, `numpy` — data manipulation
- `matplotlib`, `seaborn` — visualization (dark theme)
- `scikit-learn` — ML models, cross-validation, evaluation metrics

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/iris-botanist-classifier.git
cd iris-botanist-classifier

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn

# Launch the notebook
jupyter notebook Iris_Botanist_Classifier.ipynb
```

> Make sure `Iris.csv` is in the same directory as the notebook before running.

---

## 📈 Visualizations Included

| # | Chart | Purpose |
|---|---|---|
| 1 | Mean Feature Comparison (Grouped Bar) | Inter-species measurement differences |
| 2 | Pair Plot (4×4 Scatter Matrix) | Cross-variable relationships and separability |
| 3 | Petal Box Plots | Variance and overlap analysis |
| 4 | Petal Scatter + Decision Boundaries | Visual validation of threshold rules |
| 5 | Model Accuracy Comparison (Bar) | Cross-validated accuracy across 4 models |
| 6 | Confusion Matrix | Best model misclassification breakdown |
| 7 | Feature Importance (Horizontal Bar) | Random Forest feature contribution scores |

---

## 📄 License

This project is open for educational and research use. Dataset credit: UCI Machine Learning Repository.

---

*Data Science Capstone — Analytics & Insights Division | June 2026*
