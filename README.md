
# Phishing Detector

## Introduction

Phishing attacks represent one of the most prevalent cybersecurity threats, where attackers create fraudulent websites that mimic legitimate ones to steal sensitive information like passwords, credit card numbers, and personal data. This project implements a machine learning-based phishing detection system that analyzes various website features to classify URLs as legitimate or phishing attempts.

The detector uses a comprehensive dataset with 30 features extracted from websites, including URL characteristics, security indicators, and behavioral patterns. By leveraging multiple machine learning algorithms, the system can effectively identify malicious websites with high accuracy.

## Features

The system analyzes various website characteristics, including:

- **URL-based features**: IP address usage, URL length, shortening services, special characters
- **Domain features**: Domain registration length, subdomain usage, SSL certificate status
- **Content features**: Favicon usage, port configuration, HTTPS tokens, anchor links
- **Security indicators**: DNS records, page rank, Google indexing status
- **Behavioral patterns**: Pop-up windows, iframe usage, redirections

Example features:
- `having_IP_Address`: Whether the URL uses IP address instead of domain name
- `URL_Length`: Categorized length of the URL (short/medium/long)
- `SSLfinal_State`: SSL certificate status and validity
- `Domain_registeration_length`: How long the domain has been registered

## Algorithms Used

### 1. Logistic Regression
A linear classifier that uses the logistic function to model binary classification. It estimates the probability of a website being phishing based on a linear combination of features. The algorithm is interpretable and works well for linearly separable data.

### 2. K-Nearest Neighbors (KNN)
A non-parametric algorithm that classifies websites based on the majority class of their k nearest neighbors in the feature space. It's effective for capturing local patterns in the data and doesn't make assumptions about data distribution.

### 3. Naive Bayes (Multinomial)
A probabilistic classifier based on Bayes' theorem with the assumption of feature independence. Despite the independence assumption, it often performs well in practice and is particularly suitable for discrete/categorical features like those in this dataset.

### 4. Support Vector Machine (SVM)
Uses the Radial Basis Function (RBF) kernel to find the optimal hyperplane that separates phishing and legitimate websites in a high-dimensional space. SVM is effective for complex decision boundaries and works well with the transformed feature space.

### 5. Multi-Layer Perceptron (MLP)
A neural network with hidden layers that can learn non-linear relationships between features. The network uses backpropagation to learn complex patterns and interactions between website characteristics that simpler algorithms might miss.

## Model Selection

Model selection was performed using a stratified 5-fold cross-validation approach to ensure robust evaluation across different subsets of the data. The origilnal dataset was split into training and test sets, with 80% of the data used for training and 20% for testing.

The training set (80% of the data) was further split training set (70% of the total dataset) and deployment set (10% of the total dataset). The deployment set was used to evaluate the final model's performance on unseen data after the model selection process.

## Performance

The system achieves strong performance across all algorithms:
| **Algorithm** | **Score (Validation)** | **Score (Deployment)** |
|---------------|--------------|--------------|
| **SVM** | 96.4% | 96.5% |
| **MLP Classifier** | 96.4% | 96.3% |
| **KNN** | 95.5% | 96.2% |
| **Logistic Regression** | 92.8% | 92.9% |
| **Naive Bayes** | 88.6% | 89.1% |

The SVM classifier, with this parameters setup: *{C=10, gamma=0.1, kernel='rbf'}*, was selected as the final model and used to train the entire training set (80% of the initial dataset) and test on the test set (data never seen during the training and model selection phase).

| **Accuracy** | **Precision** | **Recall** | **F1-Score** |
|--------------|---------------|------------|--------------|
| 96.4%        | 96.4%         | 96.5%      | 96.4%        |


