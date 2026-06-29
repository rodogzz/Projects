# Machine Learning, Data Science, and Optimization Projects

This repository contains a portfolio of selected projects focused on machine learning, deep learning, data science, and metaheuristic optimization. The projects cover supervised learning, unsupervised learning, neural network training, transfer learning, time series forecasting, and optimization-based model training.

The main goal of this repository is to document practical implementations of machine learning techniques applied to different types of problems, while also showing the complete workflow of experimentation, evaluation, and interpretation of results.

---

## Featured Projects

### 1. Multi-Label Scene Classification

This project focuses on the classification of natural scene images where each image may belong to more than one category at the same time. The target labels include categories such as desert, sunset, mountains, sea, and trees.

A convolutional neural network approach is implemented for the multi-label classification task, including both a baseline CNN model and a transfer learning model based on a pre-trained architecture. Since the problem is multi-label, the model uses sigmoid outputs and binary cross-entropy loss, allowing each label to be predicted independently.

The project includes data preprocessing, model training, evaluation using multi-label metrics, and visual inspection of predictions.

**Main topics:**

- Multi-label image classification
- Convolutional Neural Networks
- Transfer Learning
- Binary cross-entropy loss
- Sigmoid-based multi-label prediction
- Evaluation with Hamming Loss, Subset Accuracy, F1-score, Precision, and Recall

**Technologies:** Python, TensorFlow, Keras, NumPy, Scikit-learn, Matplotlib

---

### 2. Large-Scale Accident Clustering

This project applies unsupervised learning techniques to a large-scale accident dataset in order to identify meaningful accident patterns and groups.

The workflow includes data preprocessing, feature selection, dimensionality reduction using PCA, and clustering using density-based and hierarchical methods. HDBSCAN is used to discover clusters of arbitrary shape while also identifying noisy observations, while Ward hierarchical clustering is evaluated on smaller samples due to its computational cost.

The project emphasizes scalability, interpretability, and the comparison of clustering quality metrics such as Silhouette Score, Davies-Bouldin Index, and Calinski-Harabasz Score.

**Main topics:**

- Large-scale data preprocessing
- Dimensionality reduction with PCA
- Density-based clustering with HDBSCAN
- Hierarchical clustering with Ward linkage
- Cluster evaluation and interpretation
- Handling noisy observations in unsupervised learning

**Technologies:** Python, Pandas, NumPy, Scikit-learn, HDBSCAN, PCA, Matplotlib

---

### 3. PSO-Based Neural Network Training

This project explores the use of Particle Swarm Optimization as an alternative method for training neural networks.

Instead of relying only on traditional gradient-based optimization, the neural network weights are optimized using a population-based metaheuristic. The project compares PSO-based training against conventional gradient descent approaches, analyzing both predictive performance and computational behavior.

The implementation includes the representation of neural network weights as particles, the definition of a fitness function based on prediction error, and the update of particle positions and velocities using inertia, cognitive, and social components.

**Main topics:**

- Particle Swarm Optimization
- Neural network weight optimization
- Metaheuristic training of machine learning models
- Comparison with gradient-based learning
- Fitness-based optimization
- Classification using multilayer perceptrons

**Technologies:** Python, NumPy, Scikit-learn, Machine Learning, Metaheuristics

---

### 4. Memetic Optimization for Financial Time Series Forecasting

This project presents a memetic optimization framework for training a recurrent neural network applied to financial time series forecasting.

The proposed approach combines Differential Evolution for global exploration with the Fletcher-Reeves conjugate gradient method for local refinement. Instead of training the neural network using traditional backpropagation, the model parameters are directly optimized through a hybrid metaheuristic strategy.

The forecasting task focuses on predicting future closing prices for different time horizons. The project evaluates the behavior of the proposed memetic method against a standard Differential Evolution approach and compares the results with previous work from the literature.

**Main topics:**

- Financial time series forecasting
- Recurrent Neural Networks
- Differential Evolution
- Fletcher-Reeves conjugate gradient method
- Memetic algorithms
- Direct optimization of neural network weights
- Forecasting horizons and error analysis

**Technologies:** Python, NumPy, PyTorch, Pandas, Matplotlib, Metaheuristic Optimization

---

## Repository Purpose

This repository is intended to serve as a technical portfolio of applied machine learning and optimization projects. Each project demonstrates a different type of problem, methodology, and evaluation strategy:

| Project | Type of Problem | Main Approach |
|--------|-----------------|---------------|
| Multi-Label Scene Classification | Supervised Learning / Computer Vision | CNN and Transfer Learning |
| Large-Scale Accident Clustering | Unsupervised Learning | PCA, HDBSCAN, Ward Clustering |
| PSO-Based Neural Network Training | Optimization / Classification | Particle Swarm Optimization |
| Memetic Optimization for Forecasting | Time Series Forecasting / Optimization | Differential Evolution + Fletcher-Reeves |

---

## Skills Demonstrated

Across the projects, this repository demonstrates practical experience with:

- Machine learning model development
- Deep learning for image classification
- Transfer learning with pre-trained neural networks
- Multi-label classification metrics
- Unsupervised learning and clustering evaluation
- Large-scale dataset preprocessing
- Metaheuristic optimization algorithms
- Neural network weight optimization
- Time series forecasting
- Experimental comparison and result interpretation
- Technical documentation for reproducible projects

---

## Technologies Used

The projects in this repository use a combination of scientific computing, machine learning, and deep learning tools, including:

- Python
- NumPy
- Pandas
- Scikit-learn
- TensorFlow
- Keras
- PyTorch
- HDBSCAN
- Matplotlib
- Jupyter Notebook

---

## Project Structure

Each project is organized in its own directory and includes the corresponding source code, notebooks, experiments, models, and documentation when applicable.

A typical project structure may include:

```text
project-name/
├── data/
├── notebooks/
├── models/
├── results/
├── README.md
└── requirements.txt
