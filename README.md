 ### Medical Data Analysis & Preprocessing Project

This repository contains two complementary projects focusing on medical dataset exploration and machine learning preprocessing pipeline creation.

The workflow is structured as:

Exploratory Data Analysis (EDA): Understand the dataset, visualize patterns, and detect correlations.

Data Preprocessing with Pipeline: Clean, transform, and prepare the dataset for machine learning models using a robust, reusable pipeline.

Project 1: Exploratory Data Analysis (EDA)
Overview

The goal of this project is to explore and visualize a medical dataset containing information such as treatment duration, patient age, gender, and application times.

Key Steps
Data Cleaning

Removed duplicate rows

Converted treatment and application durations into numerical features

Handled missing values

Exploratory Analysis

Treatment Sessions Distribution: Frequency counts of treatment session numbers

Age Distribution: Histogram and KDE (Kernel Density Estimation)

Treatment Duration by Gender: Boxplot comparison

Correlation Analysis: Heatmap showing relationships between numerical features

Visualizations

Count plot of treatment session counts

Histogram of age distribution

Boxplot of treatment duration by gender

Correlation heatmap of numerical variables

These plots help identify trends in treatment durations, age demographics, and gender-related patterns.

Project 2: Data Preprocessing with Pipeline
Overview

This project implements a robust data preprocessing pipeline to prepare the dataset for machine learning models. It ensures reproducibility, scalability, and safe handling of categorical and numerical variables.

Components
Custom Safe Label Encoder (GuvenliEtiketleyici)

Encodes categorical features

Handles missing values as a separate category

Assigns -1 to unseen categories in test data

Comprehensive Data Cleaning (VeriOnIsleyici class)

Removes unnecessary columns (HastaNo, KanGrubu)

Handles missing values in categorical columns with logical replacements

Converts UygulamaSuresi into numeric minutes

Fills missing gender values with the mode

Removes duplicates

Pipeline Construction

Numerical features: imputation (median) + standard scaling

Categorical features: imputation (constant) + safe label encoding

Combined with ColumnTransformer and integrated into a Scikit-learn Pipeline

Training/Test Split

Stratified split by the target variable

Preprocessed training and test sets ready for model training

Output

After running the pipeline, you get:

Preprocessed training set (X_egitim_islenmis)

Preprocessed test set (X_test_islenmis)

Corresponding target variables (y_egitim, y_test)

Technologies Used

Python 3.x

Libraries

pandas, numpy for data manipulation

matplotlib, seaborn for visualization

scikit-learn for preprocessing and pipeline construction

Usage
Run Exploratory Data Analysis
python eda_script.py

Run Data Preprocessing Pipeline
python preprocessing_pipeline.py


Both scripts can be adapted with different dataset paths by modifying the DOSYA_YOLU variable inside the code.

Next Steps

Integrate machine learning models (e.g., Logistic Regression, Random Forest, Gradient Boosting)

Automate EDA reporting with libraries such as ydata-profiling

Deploy preprocessing pipeline with joblib for production
