# Quantum Convolutional Neural Networks (QCNN) for Image Classification

This project explores the use of **Quantum Machine Learning (QML)** techniques for image classification within the constraints of current quantum hardware (NISQ era).

Specifically, we implement a **Quantum Convolutional Neural Network (QCNN)** inspired by classical CNN architectures, and evaluate its ability to distinguish between simple synthetic image patterns.

## Motivation

Classical Convolutional Neural Networks (CNNs) are highly effective in computer vision tasks due to:

* Local feature extraction (convolutions)
* Hierarchical representation learning
* Dimensionality reduction (pooling)

However, translating these concepts into the quantum domain is non-trivial due to:

* The unitary nature of quantum evolution
* The no-cloning theorem
* Measurement constraints

This project investigates how **CNN-like inductive biases** can be adapted into quantum circuits.

## Problem Definition

Instead of using high-dimensional real-world images (e.g., 200×200×3), which are currently infeasible for quantum hardware, we define a simplified classification task:

* Input: synthetic grayscale images
* Size: small grids (e.g., 2×2 or 4×4)
* Classes:

  * **Horizontal stripe**
  * **Vertical stripe**

Each image is flattened and encoded into a quantum state.

## Methodology

### 1. Data Encoding (Feature Map)

Classical data is embedded into a quantum state using a parameterized feature map:

* Initial approach: `ZFeatureMap`
* Improved approach: `ZZFeatureMap`

The latter introduces entanglement and significantly improves performance.

### 2. QCNN Architecture

The model is built as a sequence of:

#### Quantum Convolution Layers

* Local parameterized 2-qubit circuits
* Applied to neighboring qubits
* Capture local correlations (analogous to classical filters)

#### Quantum Pooling Layers

* Reduce effective dimensionality
* Transfer information from “source” qubits to “sink” qubits
* No measurement (to preserve quantum information)

The architecture follows a hierarchical structure:

### 3. Observable-Based Classification

Instead of classical logits, the model outputs the **expectation value of a quantum observable**

* (U(theta)): QCNN circuit
* (O): observable (e.g., Pauli-Z)

### 4. Label Representation (Critical Insight)

To ensure consistency with quantum outputs:

* Labels are mapped to:

  * **+1** (class A)
  * **-1** (class B)


### 5. Training

The model is trained by minimizing a loss function (e.g., MSE):

L(theta) = (y_pred - y_real)**2


Optimization is performed using classical optimizers such as:

* COBYLA (gradient-free)


## Results

Using:

* ZZFeatureMap
* Balanced dataset
* Proper label mapping ({-1, +1})

We achieve:

* **~100% accuracy** on the test set
* Clear separation in observable space:

  * Positive expectation values for one class
  * Negative values for the other

This demonstrates that QCNNs can successfully learn structured patterns even in constrained settings.


## Key Insights

* **Label encoding must match observable range**
  (critical for successful training)

* **Feature map choice is crucial**
  (ZZFeatureMap significantly outperforms ZFeatureMap)

* **Model depth and qubit count affect trainability**
  (larger systems introduce optimization challenges)

* **Observable defines the output space**
  (unlike classical neural networks)


## Limitations

* Small input size due to NISQ constraints
* Simulation-based experiments (not hardware execution)
* Scalability remains an open challenge
* Sensitive to initialization and optimizer choice


## Future Work

* Scaling to larger qubit systems (e.g., 16+ qubits)
* Patch-based quantum encoding (hybrid CNN-QCNN)
* Alternative feature maps and ansätze
* Hardware execution and noise analysis
* Comparison with classical baselines



## Installation


pip install qiskit qiskit-machine-learning numpy matplotlib scikit-learn



## Usage

Run the main notebook to:

1. Generate dataset (You can change de size of the image)
2. Build QCNN (If you change de size, you have to make some changes on de observable)
3. Train model
4. Evaluate performance



## References

* Cong et al., *Quantum Convolutional Neural Networks* (Nature Physics, 2019)
* Qiskit Machine Learning Documentation
* Schuld & Petruccione, *Supervised Learning with Quantum Computers*



## Final Remarks

This project provides a practical demonstration that:

> Quantum circuits can be structured to mimic deep learning architectures and successfully learn from data, even under current hardware limitations.

Quantum machine learning is still in its early stages, but results like these suggest a promising direction for future research.

