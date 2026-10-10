# Mobile Robot Surface Classification Using Machine Learning

## Overview

This project explores the use of Machine Learning to identify the type of surface a mobile robot is moving across using onboard sensor data.

The goal is to classify different ground surfaces based on inertial measurements and motion-related signals, without relying on external cameras or environmental perception systems.

The project was developed as a final assignment for the **Machine Learning** course of the Master's Degree in Robotics and Automation.

## Objectives

- Develop a surface classification pipeline using sensor data collected from a mobile robot.
- Analyze inertial sensor signals and identify patterns associated with different ground materials.
- Address class imbalance and improve model generalization.
- Compare feature engineering strategies and classification algorithms.
- Generate predictions in the required Kaggle submission format.

## Dataset

The dataset contains time-series measurements grouped by `series_id`. Each series represents a robot trajectory segment associated with a single surface label.

The input features include:

- **Orientation:** Quaternion components (X, Y, Z, W).
- **Angular velocity:** X, Y and Z axes.
- **Linear acceleration:** X, Y and Z axes.

Each trajectory contains 128 measurements per sensor, providing information about the robot's movement, orientation and interaction with the ground.

The classification task involves nine surface classes.

## Methodology

### 1. Exploratory Data Analysis

The first stage focuses on understanding the dataset and the physical meaning of the sensor measurements.

- Inspecting dataset structure and sensor variables.
- Analyzing class distribution and identifying imbalances.
- Visualizing time-series signals to study vibration patterns and temporal variability.
- Comparing sensor distributions across different surfaces.
- Examining correlations between variables to identify redundancy and complementary information.

### 2. Data Preprocessing

The preprocessing pipeline transforms raw measurements into a suitable representation for classification.

- Encoding surface labels using `LabelEncoder`.
- Grouping measurements by `series_id`.
- Reshaping each trajectory into a feature vector.
- Splitting the data into training and validation subsets.
- Applying SMOTE to the training data to mitigate class imbalance.

The initial approach represents each trajectory using its raw sensor measurements, resulting in a high-dimensional feature space.

### 3. Baseline Model

A Random Forest classifier is implemented as the baseline model.

This provides a reference for evaluating whether feature engineering improves classification performance.

The baseline uses raw time-series measurements and is evaluated using classification reports and confusion matrices.

### 4. Feature Engineering

Several feature engineering strategies are explored to improve the representation of the robot's physical interaction with the ground.

**Statistical features**

- Mean and variance.
- Standard deviation.
- Minimum and maximum values.
- Signal range and other descriptive statistics.

**Motion magnitude**

The Euclidean magnitudes of the linear acceleration and angular velocity vectors are calculated to capture overall motion intensity while reducing dependence on individual sensor axes.

**Orientation representation**

Quaternion-based orientation measurements are transformed into Euler angles (roll, pitch and yaw) to investigate their influence on classification performance.

**Vibration-focused features**

An experimental approach emphasizes vertical acceleration and the absolute differences between consecutive measurements to capture vibration and impact patterns associated with surface irregularities.

### 5. Model Optimization

Random Forest is optimized using `GridSearchCV` and `RandomizedSearchCV`, depending on the experiment.

The hyperparameter search explores:

- Number of trees.
- Maximum tree depth.
- Minimum samples required for node splitting and leaf nodes.
- Split criteria.
- Class weighting.

A feedforward neural network is also implemented using TensorFlow and Keras to compare its performance against the tree-based approach.

### 6. Evaluation

Model performance is assessed using:

- Accuracy.
- Precision, recall and F1-score.
- Confusion matrices.
- Per-class performance analysis.

Special attention is given to minority classes, since overall accuracy alone can hide poor performance on underrepresented surfaces.

### 7. Prediction and Submission

The final stage applies the selected preprocessing and feature engineering steps to the test dataset.

Predictions are converted back into surface labels and exported as CSV files compatible with the required Kaggle submission format.

Multiple submission versions are generated to compare alternative feature engineering approaches.

## Technologies Used

- **Python** — Main programming language.
- **Pandas and NumPy** — Data manipulation and numerical processing.
- **Matplotlib and Seaborn** — Data visualization and exploratory analysis.
- **Scikit-learn** — Preprocessing, classification, model selection and evaluation.
- **imbalanced-learn** — SMOTE-based class balancing.
- **TensorFlow / Keras** — Neural network implementation.
- **Jupyter Notebook** — Experimental workflow and documentation.

## Project Structure

```text
.
├── README.md
├── X_train.csv
├── X_test.csv
├── y_train.csv
├── sample_submission.csv
└── surface_classification.ipynb
```

*Note: Update the filenames above to match the actual contents of the repository.*

## How to Run

### 1. Clone the repository

```bash
git clone <repository-url>
cd <repository-folder>
```

### 2. Install the dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn tensorflow jupyter
```

### 3. Prepare the dataset

Place the required CSV files in the notebook's working directory.

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the notebook and execute the cells sequentially to reproduce the analysis, feature engineering experiments, model training and prediction generation.

**Note:** The original dataset files are required to execute the complete workflow. Obtain them from the corresponding dataset source if they are not included in this repository.

## Key Takeaways

This project demonstrates an end-to-end Machine Learning workflow applied to mobile robotics, combining sensor data analysis, physical signal interpretation, feature engineering and supervised classification.

The main takeaway is that carefully designed features can provide a more effective representation than raw sensor measurements alone. Statistical descriptions of acceleration and angular velocity can help capture the robot's interaction with different ground surfaces.

The project also highlights the importance of class imbalance, per-class evaluation and experimental comparison when developing classification systems for real-world robotic applications.

## Author

**Marcos del Cerro Villanueva**

Master's Degree in Robotics and Automation

Interested in robotics, autonomous systems, sensor processing and intelligent control.
