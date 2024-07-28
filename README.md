# CS771 - Introduction to Machine Learning - Assignment on Physically Unclonable Function
## PUF
A Physical Unclonable Function (PUF) is a technology that utilizes inherent randomness from the manufacturing process to provide a unique identifier or "fingerprint" for a physical device. PUFs are valuable in various applications, including anti-counterfeiting, device identification, authentication, key generation, and complex protocols like oblivious transfer, key exchange, and virtual proof of reality. This review discusses the development of PUFs, particularly those that use optical properties, circuit time-delays, and volatile or non-volatile memory features. It examines the diverse applications of PUFs, addresses the security challenges they face, and outlines known attacks and possible countermeasures. The review also highlights key areas for future development, such as improving bit-specific reliability, enabling reconfigurability, and integrating with public key infrastructure.

## Arbiter PUF Linear Model

This repository contains solutions and analyses related to Physical Unclonable Functions (PUFs) and machine learning techniques for predicting signal arrival times and responses. The focus is on deriving mathematical models for arbiter PUFs and COCO-PUFs, determining the required dimensionality for linear models, and conducting experiments using `LinearSVC` and `LogisticRegression` classifiers.

### Objective
To derive a linear model that predicts the time taken for the upper signal to reach the finish line in an arbiter PUF based on a 32-bit challenge vector.

### Key Equations
- **Difference Time:**  
  $$\Delta u_i = (1 - 2C_i)\Delta_{i-1} + (q_i - p_i + s_i - r_i)C_i + p_i - q_i$$
- **Combined Time:**  
  $$S_i = S_{i-1} + C_i(s_i + r_i - p_i - q_i) + p_i + q_i$$
- **Upper Signal Time:**  
  $$t_{u31} = \frac{(\Delta_{31} + S_{31})}{2}$$

### Dimensionality
The model requires 63 dimensions, as feature $x'_{31}$ can be integrated into other variables.

## COCO-PUF Linear Model

### Objective
To derive a linear model predicting the response for a COCO-PUF, using linear combinations of challenge-response pairs.

### Key Equations
- **Response Calculation:**  
  $$\Delta u_i = (1 - C_i)\Delta_{i-1} + C_i(s_i - r_i - \Delta_{i-1})$$

### Dimensionality  
Similar to the arbiter PUF model, the dimensionality required is 63.

## Experimental Analysis

### Objective
To evaluate the impact of various hyperparameters on training time and test accuracy using `LinearSVC` and `LogisticRegression`.

### Key Findings
- **LinearSVC (Hinge vs. Squared Hinge Loss)**
  - **Hinge:** Test Accuracy: Response0: 98.36%, Response1: 99.49%
  - **Squared Hinge:** Test Accuracy: Response0: 98.02%, Response1: 99.72%
- **Effect of C (Regularization Parameter)**
  - **Low C (0.01):** Reduced accuracy, faster training time.
  - **Medium C (1):** Optimal balance of accuracy and training time.
  - **High C (100):** Slight overfitting observed, marginal accuracy improvement.
- **Logistic Regression**
  - Similar trends as `LinearSVC` with slight improvements in test accuracy at higher `C` values.
