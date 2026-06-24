# Large-Scale Traffic Accident Clustering

This project applies unsupervised learning techniques to analyze and cluster large-scale traffic accident records from the **US Accidents** dataset. The main objective is to identify accident patterns using geographical, weather-related, road-condition, and traffic-control features.

The project compares density-based and hierarchical clustering approaches after preprocessing the data and applying dimensionality reduction with Principal Component Analysis (PCA).

---

## Project Overview

Traffic accident datasets usually contain high-dimensional, noisy, and heterogeneous information. This project explores how clustering algorithms can be used to group accident records with similar characteristics and support exploratory analysis of large-scale accident data.

The workflow includes:

* Data loading and sampling from a large accident dataset.
* Feature selection using numerical and boolean accident-related attributes.
* Missing value handling and preprocessing.
* Outlier treatment for selected numerical variables.
* Feature scaling.
* Dimensionality reduction using PCA.
* Clustering with HDBSCAN.
* Clustering with Ward hierarchical clustering.
* Evaluation using internal clustering metrics.
* Visualization of clustering results.

---

## Dataset

This project uses the **US Accidents** dataset.

Due to file size limitations, the dataset is not included in this repository. To run the project, download the dataset manually and place the CSV file in the following location:

```text
data/US_Accidents_March23.csv
```

The notebook is configured to work with a sample of the dataset instead of loading the full file into memory.

---

## Selected Features

The clustering process uses a subset of numerical, geographical, weather-related, and road-condition features:

```python
[
    "Start_Lat",
    "Start_Lng",
    "Distance(mi)",
    "Temperature(F)",
    "Humidity(%)",
    "Pressure(in)",
    "Visibility(mi)",
    "Wind_Speed(mph)",
    "Bump",
    "Crossing",
    "Give_Way",
    "Junction",
    "Railway",
    "Roundabout",
    "Stop",
    "Traffic_Signal"
]
```

These features were selected to represent accident location, weather conditions, visibility, road characteristics, and nearby traffic-control elements.

---

## Methodology

### 1. Data Preprocessing

The preprocessing stage includes:

* Loading a sample of the dataset.
* Selecting relevant clustering features.
* Converting boolean variables into numerical values.
* Handling missing values.
* Treating extreme outliers in selected numerical variables.
* Scaling the data using standardization.

This step ensures that all features are numerically suitable for distance-based clustering algorithms.

---

### 2. Dimensionality Reduction

Principal Component Analysis is applied to reduce dimensionality while preserving most of the information from the original feature space.

The PCA transformation is configured to preserve approximately:

```text
90% of the explained variance
```

This helps reduce computational cost and improve clustering performance, especially when working with large samples.

---

### 3. HDBSCAN Clustering

HDBSCAN is used as a density-based clustering algorithm. This method is useful for datasets where clusters may have irregular shapes and where some records may not belong clearly to any cluster.

One advantage of HDBSCAN is that it can identify noise points, assigning them the label:

```text
-1
```

This is especially useful for accident data, where some records may behave as outliers or isolated observations.

---

### 4. Ward Hierarchical Clustering

Ward hierarchical clustering is also applied to evaluate a fixed-number clustering approach.

Different values of `k` are tested, and clustering quality is compared using internal validation metrics.

---

## Evaluation Metrics

The project uses internal clustering metrics to evaluate the quality of the generated clusters:

### Silhouette Score

Measures how similar each point is to its own cluster compared to other clusters.

Higher values indicate better-defined clusters.

### Davies-Bouldin Score

Measures the average similarity between each cluster and its most similar cluster.

Lower values indicate better clustering separation.

### Calinski-Harabasz Score

Measures the ratio between between-cluster dispersion and within-cluster dispersion.

Higher values generally indicate better-defined clusters.

---

## Repository Structure

```text
.
├── Proyecto_Final.ipynb
├── README.md
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── data/
├── outputs/
├── salida/
└── salida_contenedor/
```

The following folders are ignored by Git:

```text
data/
outputs/
salida/
salida_contenedor/
```

This avoids uploading large datasets and generated output files to the repository.

---

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd <repository-folder>
```

Create a virtual environment if desired:

```bash
python -m venv .venv
source .venv/bin/activate
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## How to Run

### Option 1: Run with Jupyter Notebook

Open the notebook:

```bash
jupyter notebook Proyecto_Final.ipynb
```

Then run the cells sequentially.

Before running the notebook, make sure the dataset is located at:

```text
data/US_Accidents_March23.csv
```

---

### Option 2: Run with Docker

If Docker is available, the project can also be executed using Docker Compose.

Build the container:

```bash
docker compose build
```

Run the container:

```bash
docker compose up
```

This provides a reproducible environment for running the project without manually installing all dependencies in the local system.

---

## Outputs

The project generates visualizations and clustering results during execution.

Generated files should be saved in an output directory such as:

```text
outputs/
```

or, depending on the current notebook version:

```text
salida/
```

These folders are ignored by Git because the results can be regenerated by running the notebook.

---

## Main Techniques Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* HDBSCAN
* Principal Component Analysis
* Hierarchical clustering
* Docker

---

## Project Relevance

This project demonstrates the application of unsupervised machine learning methods to large-scale real-world data. It includes important machine learning workflow components such as preprocessing, dimensionality reduction, clustering, validation, and visualization.

The project is relevant for:

* Exploratory data analysis.
* Large-scale data preprocessing.
* Unsupervised learning.
* Pattern discovery in traffic accident data.
* Clustering evaluation.
* Reproducible machine learning workflows using Docker.

---

## Notes

The dataset is not included in this repository due to its size.

To reproduce the results, download the dataset and place it in:

```text
data/US_Accidents_March23.csv
```

The folders containing data and generated outputs are intentionally excluded from version control through `.gitignore`.

---

## Outputs and Reproducibility

The notebook includes previously generated outputs to document the results obtained during execution.

Due to the computational cost and the need for a high-resource environment, the generated output folders are not included in this repository. However, the notebook preserves the main tables, figures, and clustering results for review.

To reproduce the full experiment, download the dataset, place it under `data/US_Accidents_March23.csv`, install the dependencies, and run the notebook in a suitable local or server environment.

---

## Author

Rodolfo González
