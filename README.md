# Spam Detection: Experimental Comparison of Learning Algorithms

[![Python 3.12](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

A comprehensive experimental comparison of three supervised learning algorithms for email spam detection using the Spambase dataset from UCI Machine Learning Repository.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Algorithms](#algorithms)
- [Results](#results)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Statistical Analysis](#statistical-analysis)
- [Key Findings](#key-findings)
- [Technologies](#technologies)
- [References](#references)

---

## 🎯 Overview

This project systematically compares **Decision Tree**, **Naive Bayes**, and **Support Vector Machine (SVM)** classifiers for spam email detection. The evaluation uses stratified 10-fold cross-validation and focuses on:

- ⏱️ **Computational Performance** (Training Time)
- 🎯 **Predictive Performance** (Accuracy & F-measure)
- 📊 **Statistical Significance** (Friedman & Nemenyi Tests)

---

## 📊 Dataset

### Spambase Dataset

- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Spambase)
- **Instances:** 4,601 emails
- **Features:** 57 continuous attributes
  - 48 word frequency features
  - 6 character frequency features
  - 3 capital letter sequence features
- **Classes:** Binary (Spam = 1, Non-spam = 0)
  - Non-spam: 2,788 emails (60.6%)
  - Spam: 1,813 emails (39.4%)

---

## 🤖 Algorithms

### 1. Decision Tree
- Non-parametric supervised learning
- Recursive binary splitting based on information gain
- Interpretable tree structure
- **Implementation:** `sklearn.tree.DecisionTreeClassifier`

### 2. Naive Bayes
- Probabilistic classifier based on Bayes' theorem
- Assumes feature independence
- Very fast training
- **Implementation:** `sklearn.naive_bayes.GaussianNB`

### 3. Support Vector Machine (SVM)
- Maximum-margin classifier with RBF kernel
- Effective in high-dimensional spaces
- Computationally intensive
- **Implementation:** `sklearn.svm.SVC`

---

## 🏆 Results

### Training Time (Speed)

| Rank | Algorithm | Avg. Rank | Avg. Time (sec) |
|------|-----------|-----------|-----------------|
| 🥇 | **Naive Bayes** | 1.00 | ~0.006 |
| 🥈 | **Decision Tree** | 2.00 | ~0.062 |
| 🥉 | **SVM** | 3.00 | ~0.229 |

- **Friedman Test:** χ²_F = 20.00, p = 0.000045 ✅ **SIGNIFICANT**
- **Finding:** Naive Bayes is significantly faster than SVM

### Accuracy

| Rank | Algorithm | Avg. Rank | Avg. Accuracy |
|------|-----------|-----------|---------------|
| 🥇 | **SVM** | 1.10 | **93.4%** |
| 🥈 | **Decision Tree** | 1.90 | 91.1% |
| 🥉 | **Naive Bayes** | 3.00 | 81.3% |

- **Friedman Test:** χ²_F = 18.20, p = 0.000112 ✅ **SIGNIFICANT**
- **Finding:** Naive Bayes significantly worse than both SVM and Decision Tree

### F-measure

| Rank | Algorithm | Avg. Rank | Avg. F-measure |
|------|-----------|-----------|----------------|
| 🥇 | **SVM** | 1.10 | **91.5%** |
| 🥈 | **Decision Tree** | 1.90 | 88.9% |
| 🥉 | **Naive Bayes** | 3.00 | 80.5% |

- **Friedman Test:** χ²_F = 18.20, p = 0.000112 ✅ **SIGNIFICANT**
- **Finding:** Same pattern as accuracy

---

## 🔧 Installation

### Prerequisites
- Python 3.7+
- pip package manager

### Install Dependencies

```bash
# Clone the repository
git clone https://github.com/yourusername/spam-detection-ml.git
cd spam-detection-ml

# Install required packages
pip install numpy pandas scikit-learn scipy matplotlib jupyter
```

### Download Dataset

1. Visit [UCI Spambase Dataset](https://archive.ics.uci.edu/ml/datasets/Spambase)
2. Download `spambase.data`
3. Place in project root directory

---

## 🚀 Usage

### Run Jupyter Notebook

```bash
# Launch Jupyter Notebook
jupyter notebook

# Open code.ipynb and run all cells
```

### Run as Python Script

```bash
# If exported as .py file
python code.py
```

### Expected Output

The notebook will:
1. Load the Spambase dataset (4,601 samples, 57 features)
2. Run 10-fold cross-validation for all algorithms (~2-5 minutes)
3. Display results tables for each metric
4. Perform Friedman statistical tests
5. Conduct Nemenyi post-hoc analysis
6. Save results to CSV files:
   - `results_training_time.csv`
   - `results_accuracy.csv`
   - `results_f_measure.csv`

---

## 📁 Project Structure

```
spam-detection-ml/
│
├── code.ipynb                    # Main Jupyter Notebook
├── spambase.data                 # Dataset (download separately)
│
├── results_training_time.csv     # Training time results
├── results_accuracy.csv          # Accuracy results
├── results_f_measure.csv         # F-measure results
│
├── README.md                     # This file
└── LICENSE                       # MIT License
```

---

## 📈 Statistical Analysis

### Friedman Test
A non-parametric statistical test used to detect differences in algorithms across multiple datasets (folds).

**Formula:**
```
χ²_F = (12N)/(k(k+1)) × [Σ(R_j²) - k(k+1)²/4]
```
Where:
- N = number of datasets (10 folds)
- k = number of algorithms (3)
- R_j = average rank of algorithm j

**Implementation:** Manually implemented (no external statistical libraries)

### Nemenyi Post-hoc Test
Applied when Friedman test shows significance (p < 0.05) to determine which pairs of algorithms differ significantly.

**Formula:**
```
CD = q_α × √(k(k+1)/(6N))
```
Where:
- q_α = critical value from studentized range statistic
- CD = Critical Difference = 1.0478 (for our experiment)

**Implementation:** Manually implemented (no external statistical libraries)

### Pairwise Comparisons

**Training Time:**
- Decision Tree vs Naive Bayes: Not significant
- Decision Tree vs SVM: Not significant  
- Naive Bayes vs SVM: **SIGNIFICANTLY DIFFERENT** ✅

**Accuracy & F-measure:**
- Decision Tree vs Naive Bayes: **SIGNIFICANTLY DIFFERENT** ✅
- Decision Tree vs SVM: Not significant
- Naive Bayes vs SVM: **SIGNIFICANTLY DIFFERENT** ✅

---

## 💡 Key Findings

### Performance Trade-offs

#### Speed Champion: Naive Bayes 🚀
- **Training Time:** ~0.006 seconds (virtually instant)
- **Best For:** Real-time applications, limited computational resources
- **Trade-off:** Lowest accuracy (81.3%)

#### Accuracy Champion: SVM 🎯
- **Accuracy:** 93.4% | F-measure: 91.5%
- **Best For:** High-accuracy requirements, offline processing
- **Trade-off:** Slowest training (~0.23 seconds)

#### Balanced Option: Decision Tree ⚖️
- **Accuracy:** 91.1% | F-measure: 88.9%
- **Training Time:** ~0.062 seconds
- **Best For:** Applications requiring good accuracy with reasonable speed

### Statistical Insights

1. **All metrics show significant differences** (p < 0.05)
2. **Naive Bayes is significantly faster** than SVM
3. **Naive Bayes is significantly less accurate** than both competitors
4. **SVM and Decision Tree** have comparable accuracy (no significant difference)
5. **Clear speed-accuracy trade-off** observed

### Practical Recommendations

| Use Case | Recommended Algorithm | Reason |
|----------|----------------------|--------|
| Real-time spam filtering | Naive Bayes | Instant classification |
| Email server (moderate traffic) | Decision Tree | Balanced performance |
| Batch processing / High accuracy | SVM | Superior predictive performance |
| Mobile/Edge devices | Naive Bayes | Minimal computational requirements |
| Cloud-based filtering | SVM | Computational resources available |

---

## 🛠️ Technologies

- **Python 3.12.7**
- **NumPy** - Numerical computing
- **Pandas** - Data manipulation and analysis
- **Scikit-learn** - Machine learning algorithms
- **SciPy** - Statistical computations
- **Matplotlib** - Data visualization (optional)
- **Jupyter Notebook** - Interactive development environment

---

## 📚 References

1. Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). Spambase [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X

2. Flach, P. (2012). *Machine Learning: The Art and Science of Algorithms that Make Sense of Data*. Cambridge University Press.

3. Demšar, J. (2006). Statistical comparisons of classifiers over multiple data sets. *Journal of Machine Learning Research*, 7, 1-30.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/yourusername/spam-detection-ml/issues).

---

## ⭐ Acknowledgments

- UCI Machine Learning Repository for providing the Spambase dataset
- Scikit-learn developers for excellent machine learning tools
- Peter Flach for comprehensive ML methodology guidance

---

**Built with ❤️ for Machine Learning research and education**
