# Multiclass Classification with Kesler's Construction

This project implements a multiclass classification model based on **Kesler's construction**, a method that extends binary linear classification to multiclass problems through pairwise comparisons between the correct class and the remaining classes.

The objective of this project is to build the classifier from first principles using Python and NumPy, evaluate it on multiple benchmark datasets, and analyze its behavior using accuracy, confusion matrices, and learning curves.

---

## Project Overview

Multiclass classification is a fundamental supervised learning problem where each input sample must be assigned to one class among several possible categories.

In this notebook, a Kesler-based classifier is implemented manually instead of relying on a built-in machine learning model. The model learns one linear discriminant function per class and updates the weights by comparing the score of the correct class against the scores of all incorrect classes.

The project includes:

* Mathematical formulation of Kesler's construction.
* Manual implementation of the training algorithm.
* Feature preprocessing and standardization.
* Evaluation on multiple multiclass datasets.
* Confusion matrices for class-level analysis.
* Learning curves to inspect the optimization process.
* Final comparison of results across datasets.

---

## Datasets

The project evaluates the classifier on five multiclass classification datasets:

| Dataset  | Source                | Number of Classes |
| -------- | --------------------- | ----------------: |
| Iris     | scikit-learn          |                 3 |
| Wine     | scikit-learn          |                 3 |
| Dry Bean | Local file in `data/` |                 7 |
| Digits   | scikit-learn          |                10 |
| Glass    | Local file in `data/` |                 6 |

The Iris, Wine, and Digits datasets are loaded directly from `scikit-learn`.

The Dry Bean and Glass datasets are included in the `data/` directory to make the project reproducible without requiring manual downloads during execution.

---

## Project Structure

The repository is expected to follow this structure:

```text
.
├── data/
│   ├── Dry_Bean_Dataset.xlsx
│   └── glass.csv
├── notebook/
│   └── kesler_multiclass_classification.ipynb
├── README.md
└── requirements.txt
```

The notebook expects the external datasets to be available in the `data/` directory. Therefore, the complete repository structure must be preserved when running the project.

Running the notebook as an isolated file may cause file path errors.

---

## Methodology

The workflow followed in the notebook is:

1. Load the dataset.
2. Split the data into training and testing sets.
3. Standardize the input features.
4. Train the Kesler-based multiclass classifier.
5. Generate predictions on the test set.
6. Evaluate performance using test accuracy.
7. Visualize results through confusion matrices.
8. Analyze the learning curve of the objective function.

The model uses an augmented feature vector to include the bias term and learns a weight vector for each class. During training, each sample is compared against all incorrect classes, following Kesler's construction.

---

## Mathematical Background

For an input sample:

$$
\mathbf{x}_i \in \mathbb{R}^{d}
$$

the augmented vector is defined as:

$$
\tilde{\mathbf{x}}_i =
\begin{bmatrix}
1 \
\mathbf{x}_i
\end{bmatrix}
\in \mathbb{R}^{d+1}
$$

For a problem with (K) classes, the model learns one weight vector per class:

$$
\mathbf{w}_k \in \mathbb{R}^{d+1}
$$

The score assigned to class (k) is:

$$
g_k(\mathbf{x}_i)
=================

\mathbf{w}_k^\top \tilde{\mathbf{x}}_i
$$

The predicted class is selected as the class with the highest score:

$$
\hat{y}_i
=========

\arg\max_k g_k(\mathbf{x}_i)
$$

During training, the model compares the true class (k) against every incorrect class (j \neq k). The margin for each comparison is defined as:

$$
\Delta_{k,j}
============

(\mathbf{w}_k - \mathbf{w}_j)^\top \tilde{\mathbf{x}}_i
$$

A positive margin means that the score of the correct class is greater than the score of the competing incorrect class.

The logistic loss for each comparison is:

$$
L_{k,j}
=======

\log\left(1 + e^{-\Delta_{k,j}}\right)
$$

The full objective function is obtained by summing this loss over all training samples and all incorrect classes:

$$
J(W)
====

\sum_{i=1}^{n}
\sum_{j \neq k}
\log\left(1 + e^{-\Delta_{k,j}}\right)
$$

where (k) is the true class of sample (i).

The weights are updated using gradient descent:

$$
W^{(t+1)}
=========

## W^{(t)}

\eta
\frac{\partial J(W)}{\partial W}
$$

where (\eta) is the learning rate.

---

## Experimental Results

The following results were obtained using the Kesler-based multiclass classifier:

| Dataset  | Number of Classes | Test Accuracy |
| -------- | ----------------: | ------------: |
| Iris     |                 3 |        1.0000 |
| Wine     |                 3 |        0.9722 |
| Dry Bean |                 7 |        0.9203 |
| Digits   |                10 |        0.9583 |
| Glass    |                 6 |        0.6977 |

The classifier achieved strong performance on most datasets, especially Iris, Wine, Dry Bean, and Digits. The Glass dataset produced the lowest accuracy, which may be related to its smaller size, class imbalance, and overlap between class distributions.

---

## Results Interpretation

The confusion matrices show that most datasets have a strong concentration of values along the main diagonal, indicating correct classification across most classes.

The learning curves show the evolution of the objective function during training. A decreasing curve indicates that the optimization process is reducing the loss over time.

For more complex or imbalanced datasets, such as Glass, accuracy should be interpreted carefully. In these cases, confusion matrices provide a more detailed view of which classes are harder to separate.

---

## How to Run the Project

1. Clone the repository:

```bash
git clone <repository-url>
cd <repository-name>
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

3. Install the dependencies:

```bash
pip install -r requirements.txt
```

4. Start Jupyter:

```bash
jupyter notebook
```

5. Open the notebook located in:

```text
notebook/kesler_multiclass_classification.ipynb
```

Make sure to open and run the project while preserving the full repository structure, especially the `data/` directory.

Run the notebook from the repository root directory so that the relative paths to the `data/` folder are resolved correctly.

---

## Requirements

The main Python libraries used in this project are:

* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* OpenPyXL
* Jupyter

All dependencies are listed in `requirements.txt`.

---

## Future Improvements

Possible improvements for future versions include:

* Adding precision, recall, and F1-score for each dataset.
* Including a comparison against standard multiclass classifiers such as Softmax Regression, Logistic Regression, SVM, or Random Forest.
* Improving numerical stability during training.
* Adding regularization or gradient clipping.
* Refactoring repeated experimental code into reusable functions.
* Moving the model implementation into a separate `src/` module.
* Adding unit tests for the training and prediction functions.
* Including cross-validation for more robust evaluation.

---

## Skills Demonstrated

This project demonstrates:

* Multiclass classification.
* Mathematical understanding of linear classifiers.
* Implementation of a machine learning algorithm from scratch.
* Numerical computing with NumPy.
* Data preprocessing with scikit-learn.
* Model evaluation using accuracy and confusion matrices.
* Experimental analysis across multiple datasets.
* Technical documentation in English.

---

## Author

Rodolfo Antonio González Salazar
