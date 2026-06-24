# Multi-Label Natural Scene Classification with Transfer Learning

This project implements a multi-label image classification pipeline for natural scene recognition. Unlike traditional multi-class classification, where each image belongs to only one class, this task allows each image to contain multiple labels simultaneously.

The objective is to identify the presence of one or more natural scene categories in each image, including:

* Desert
* Mountains
* Sea
* Sunset
* Trees

The project compares a transfer learning approach based on InceptionV3 against a convolutional neural network trained from scratch.

---

## Project Overview

The main goal of this project is to build and evaluate a deep learning model capable of assigning multiple scene labels to a single image.

The workflow includes:

1. Dataset loading and preprocessing.
2. Exploratory data analysis of label distributions.
3. Multi-label target construction.
4. Feature extraction using a pre-trained InceptionV3 model.
5. Training of a custom multi-layer perceptron classifier.
6. Training of a CNN baseline from scratch.
7. Quantitative evaluation using multi-label classification metrics.
8. Qualitative inspection of predicted labels on validation images.

---

## Dataset

The project uses a multi-label natural scene dataset containing approximately 2,000 images. Each image may be associated with one or more of the following labels:

| Label     | Description                             |
| --------- | --------------------------------------- |
| Desert    | Images containing desert landscapes     |
| Mountains | Images containing mountain scenes       |
| Sea       | Images containing sea or ocean scenes   |
| Sunset    | Images containing sunset scenes         |
| Trees     | Images containing trees or forest areas |

The dataset includes mild class imbalance, which makes macro-averaged metrics useful for evaluating label-wise performance.

---

## Problem Type

This is a **multi-label image classification** problem.

Instead of using a `softmax` output layer, the models use:

* A `sigmoid` activation function in the output layer.
* `binary_crossentropy` as the loss function.
* A prediction threshold of `0.5` to determine whether each label is present.

This setup allows the model to independently estimate the probability of each class for a given image.

---

## Methodology

### Transfer Learning Model

The main model uses **InceptionV3**, pre-trained on ImageNet, as a feature extractor. The convolutional base is used to extract image representations, which are then passed to a custom dense classifier.

The extracted features are used to train a multi-layer perceptron with sigmoid outputs for the five target labels.

Images are normalized to the `[0, 1]` range using a rescaling factor of `1/255`. The same preprocessing strategy is used consistently during feature extraction, validation, and qualitative prediction visualization.

### CNN Baseline

A second model is implemented as a baseline using a convolutional neural network trained from scratch. This baseline provides a direct comparison against the transfer learning approach.

The comparison helps evaluate the benefit of using pre-trained visual features when working with a relatively small image dataset.

---

## Evaluation Metrics

Since this is a multi-label classification problem, multiple complementary metrics are used:

| Metric          | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| Hamming Loss    | Measures the fraction of incorrectly predicted labels         |
| Subset Accuracy | Measures exact match accuracy across all labels               |
| F1 Macro        | Computes F1 independently per label and averages them equally |
| F1 Micro        | Computes F1 globally across all label decisions               |
| Precision Macro | Measures average label-wise precision                         |
| Recall Macro    | Measures average label-wise recall                            |

These metrics provide a more complete evaluation than standard accuracy alone.

---

## Results

The transfer learning model achieved stronger performance than the CNN trained from scratch across the main evaluation metrics.

| Model                              | Hamming Loss | Subset Accuracy | F1 Macro | F1 Micro | Precision Macro | Recall Macro |
| ---------------------------------- | -----------: | --------------: | -------: | -------: | --------------: | -----------: |
| Transfer Learning with InceptionV3 |       0.0785 |          0.7125 |   0.8314 |   0.8328 |          0.8950 |       0.7778 |
| CNN from Scratch                   |       0.1355 |          0.5100 |   0.6700 |   0.6816 |          0.7938 |       0.5886 |

The results show that the transfer learning approach produced lower label-level error and better F1 performance than the CNN baseline. This suggests that pre-trained feature extraction is especially useful when working with relatively small image datasets.

---

## Sample Predictions

The notebook includes qualitative visual inspection of validation images. Predicted labels are compared against the true labels to better understand model behavior beyond numerical metrics.

This step is useful for identifying cases where:

* The model predicts all labels correctly.
* The model partially detects the correct labels.
* The model misses visually ambiguous categories.
* The model predicts additional plausible labels.

---

## Repository Structure

```text
multi-label-natural-scene-classification/
├── data/
│   └── miml_dataset/
│       ├── images/
│       ├── miml_labels_1.csv
│       └── miml_labels_2.csv
├── notebooks/
│   └── Multi_Label_Classifier.ipynb
├── models/
│   └── cnn_model.keras
├── README.md
└── requirements.txt
```

Depending on file size limitations, the dataset and trained model may be excluded from the repository. In that case, the dataset should be placed manually inside the `data/miml_dataset/` directory.

---

## How to Run

1. Clone the repository:

```bash
git clone <repository-url>
cd multi-label-natural-scene-classification
```

2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

3. Place the dataset inside the following directory:

```text
data/miml_dataset/
```

4. Open the notebook:

```bash
jupyter notebook notebooks/Multi_Label_Classifier.ipynb
```

5. Run all cells from top to bottom.

---

## Technologies Used

* Python
* TensorFlow / Keras
* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* InceptionV3
* Jupyter Notebook

---

## Key Takeaways

This project demonstrates the application of transfer learning to a multi-label computer vision problem. The results show that using a pre-trained convolutional network as a feature extractor can significantly improve classification performance compared to training a CNN from scratch, especially when the dataset is relatively small.

The project also highlights the importance of using proper multi-label evaluation metrics instead of relying only on standard accuracy.
