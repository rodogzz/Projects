# MLP Training from Scratch: Backpropagation vs Particle Swarm Optimization

## Overview

This project implements a simple Multilayer Perceptron (MLP) from scratch and compares two different training strategies for multiclass classification:

1. **Backpropagation**, a conventional gradient-based optimization method.
2. **Particle Swarm Optimization (PSO)**, a population-based metaheuristic that directly optimizes the network weights.

The goal of this project is not to build a state-of-the-art classifier, but to study how two different optimization strategies behave when applied to the same neural network architecture under the same dataset and evaluation setup.

This project is intended as an educational and experimental comparison of optimization strategies for neural network training.

---

## Project Objective

The main objective is to evaluate whether a population-based optimization method such as PSO can train a small neural network competitively when compared against standard Backpropagation.

The project focuses on the following questions:

* Can PSO directly optimize the weights of a neural network without using gradient information?
* How does PSO compare against Backpropagation in terms of training error?
* Which method generalizes better on unseen test data?
* What are the trade-offs between gradient-based learning and metaheuristic-based optimization?

---

## Dataset

The experiment uses the Wine dataset available through `scikit-learn`.

The dataset contains chemical analysis measurements of wines from three different classes. Each sample is represented by 13 numerical features.

Dataset characteristics:

* **Samples:** 178
* **Features:** 13 numerical attributes
* **Classes:** 3 wine categories
* **Task:** Multiclass classification

The dataset is loaded directly from `sklearn.datasets.load_wine`, so no external dataset download is required.

---

## Methodology

The project follows a controlled experimental setup:

1. Load the Wine dataset from `scikit-learn`.
2. Standardize the input features.
3. Encode the class labels using one-hot encoding.
4. Split the dataset into training and testing sets.
5. Implement a simple MLP from scratch using NumPy.
6. Train the same MLP architecture using:

   * Backpropagation
   * Particle Swarm Optimization
7. Evaluate both models using classification and regression-style metrics.
8. Compare training performance, test performance, and generalization behavior.

---

## Neural Network Architecture

The classification model used in this project is a simple Multilayer Perceptron (MLP) designed for the Wine multiclass classification problem.

The network follows a fully connected feedforward architecture composed of an input layer, one hidden layer, and an output layer:

* **Input layer:** 13 neurons, corresponding to the 13 numerical features of the Wine dataset.
* **Hidden layer:** 4 neurons, used to learn an intermediate nonlinear representation of the input data.
* **Output layer:** 3 neurons, corresponding to the three wine classes in the dataset.

The model uses the sigmoid activation function in both the hidden and output layers.

Each input sample is propagated through the network using two weight matrices:

$$
W_1 \in \mathbb{R}^{13 \times 4}
$$

$$
W_2 \in \mathbb{R}^{4 \times 3}
$$

where (W_1) maps the input features to the hidden layer, and (W_2) maps the hidden representation to the output layer.

For simplicity, this implementation does not include bias terms.

---

## Training Strategies

### Backpropagation

Backpropagation is used as the conventional gradient-based training approach.

The network weights are updated according to the error propagated backward from the output layer to the hidden layer. The training loop stops when the training MSE reaches the defined tolerance or when the maximum number of epochs is reached.

### Particle Swarm Optimization

Particle Swarm Optimization is used as a metaheuristic alternative for training the MLP.

In this approach, all neural network weights are flattened into a single candidate solution vector. Each particle in the swarm represents a complete set of network weights. The swarm then searches the parameter space by updating each particle according to its current velocity, personal best position, and global best position.

After optimization, the best particle is unpacked back into the two original weight matrices of the MLP.

---

## Evaluation Metrics

Both training strategies are evaluated using the following metrics:

* **Training MSE**
* **Testing MSE**
* **Test Accuracy**
* **Macro Precision**
* **Macro Recall**
* **Macro F1-score**
* **Epochs / Iterations**

The use of macro-averaged metrics allows the evaluation to consider all classes equally.

---

## Results

The obtained results are summarized below:

| Method                | Training MSE | Testing MSE | Test Accuracy | Macro Precision | Macro Recall | Macro F1-score | Epochs / Iterations |
| --------------------- | -----------: | ----------: | ------------: | --------------: | -----------: | -------------: | ------------------: |
| MLP + Backpropagation |     0.009972 |    0.021747 |      0.981481 |        0.982456 |     0.984127 |       0.982861 |                 348 |
| MLP + PSO             |     0.009940 |    0.056716 |      0.907407 |        0.935897 |     0.896296 |       0.907894 |                  98 |

---

## Results Analysis

The obtained results show that both training strategies were able to optimize the MLP successfully, although they presented different behavior in terms of generalization performance.

The PSO-trained MLP achieved the lowest training MSE, with a value of **0.009940**, slightly outperforming the Backpropagation-trained MLP, which obtained a training MSE of **0.009972**. This indicates that PSO was able to find a competitive set of network weights directly in the parameter space, even without using gradient-based updates.

However, the Backpropagation-trained MLP achieved better performance on the test set. It obtained a testing MSE of **0.021747**, a test accuracy of **0.981481**, and a macro F1-score of **0.982861**. In comparison, the PSO-trained MLP obtained a higher testing MSE of **0.056716**, a test accuracy of **0.907407**, and a macro F1-score of **0.907894**.

These results suggest that, although PSO was effective at minimizing the training error, Backpropagation produced a model with stronger generalization performance on unseen data. This behavior is expected in many supervised learning scenarios, since gradient-based optimization is specifically designed to efficiently adjust neural network parameters with respect to the loss landscape.

From an optimization perspective, the results are still relevant because PSO reached a training MSE comparable to Backpropagation in fewer optimization iterations. Nevertheless, iterations and epochs are not directly equivalent in computational cost, so this result should not be interpreted as a direct runtime comparison.

Overall, this experiment shows that PSO can be used as an alternative optimization strategy for training small neural networks, but Backpropagation remains more effective in this experiment when considering test accuracy, testing MSE, and macro-averaged classification metrics.

---

## Key Findings

* PSO achieved the lowest training MSE.
* Backpropagation achieved better test performance across all classification metrics.
* The PSO-trained model showed competitive training optimization but weaker generalization.
* Direct weight optimization through PSO is feasible for a small MLP.
* Backpropagation remains more reliable for this classification task.
* Additional PSO tuning or multiple independent runs would be required to evaluate its stability more rigorously.

---

## Repository Structure

```text
mlp-backprop-vs-pso/
│
├── README.md
├── requirements.txt
├── .gitignore
│
└── notebooks/
    └── mlp_backprop_vs_pso.ipynb
```

---

## How to Run

### 1. Clone the repository

```bash
git clone <repository-url>
cd mlp-backprop-vs-pso
```

### 2. Create and activate a virtual environment

On macOS/Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Open the notebook

```bash
jupyter notebook notebooks/mlp_backprop_vs_pso.ipynb
```

or open the notebook directly in VS Code.

---

## Requirements

The main dependencies are:

```txt
numpy
pandas
matplotlib
scikit-learn>=1.2
jupyter
```

---

## Limitations

This project is intentionally simple and focused on understanding optimization strategies rather than maximizing predictive performance.

Some limitations include:

* The MLP does not include bias terms.
* The architecture is small and fixed.
* PSO is evaluated using a single configuration.
* The experiment uses a single train-test split.
* Multiple random seeds are not evaluated.
* Runtime comparison is not included.
* A standard library baseline such as `sklearn.neural_network.MLPClassifier` is not included.

---

## Future Improvements

Possible extensions of this project include:

* Adding bias terms to the MLP.
* Running multiple independent trials with different random seeds.
* Reporting mean and standard deviation of metrics across runs.
* Measuring and comparing training runtime.
* Performing hyperparameter tuning for PSO.
* Comparing against `sklearn.neural_network.MLPClassifier`.
* Moving the MLP and PSO implementations into reusable Python modules.
* Adding unit tests for core functions.
* Testing the approach on larger datasets.

---

## Conclusion

This project compared two training strategies for a manually implemented MLP classifier: standard Backpropagation and Particle Swarm Optimization. Both methods were able to train the network successfully on the Wine dataset, but they showed different strengths.

PSO obtained the lowest training MSE, which demonstrates its ability to search directly for suitable neural network weights without relying on gradient information. However, Backpropagation achieved better test performance across all classification metrics, including accuracy, macro precision, macro recall, and macro F1-score.

The results indicate that PSO is a viable optimization alternative for small neural networks and can reach competitive training error, but in this experiment Backpropagation provided better generalization.
