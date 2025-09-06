Name: Enis Kadiroğlu
E-mail: enis.kadiroglu@ogr.dpu.edu.tr

Date: 06.09.2025

###Patient Exploratory Data Analysis Report
1. Executive Summary

This report outlines the preprocessing steps applied to the projectpus.xlsx dataset.
The primary objective of preprocessing is to enhance data quality by removing duplicate records, addressing missing values, and transforming raw features into a structured format.
These steps are essential to ensure that the dataset is consistent, reliable, and suitable for exploratory analysis as well as future machine learning applications.

2. Data Cleaning and Preparation

Removal of Duplicate Records

Duplicate rows were identified using the command:

df.duplicated().sum()


To avoid bias and redundancy in the analysis, duplicates were removed with:

df.drop_duplicates()


Missing Value Detection

Missing values were examined with:

df.isnull().sum()


It was observed that variables such as Alerji, KanGrubu, and KronikHastalik had a high proportion of missing data.

These variables require careful handling in subsequent analyses to prevent misleading results.

Feature Transformation

The variables TedaviSuresi and UygulamaSuresi were originally in text format.

Numeric values were extracted using regular expressions and stored in new variables (TedaviSuresi_Sayi and UygulamaSuresi_Sayi).

This transformation enables statistical analysis and correlation measurement.

3. Results and Observations

The dataset became cleaner and more consistent after removing duplicate records.

Missing data remained an important challenge, particularly in health-related attributes, highlighting the need for imputation strategies in later modeling phases.

Feature transformations allowed previously unusable text-based variables to be analyzed numerically.

4. Conclusion and Recommendations

The preprocessing stage significantly improved the usability of the dataset.
Key findings:

Data Quality Improvement: Removal of duplicates increased reliability.

Structured Features: Text-based treatment duration and application duration were successfully converted into numeric values.

Remaining Challenge: High levels of missing data in certain medical variables should be addressed before advanced analysis.

Recommendation: Future work should focus on missing data imputation, outlier detection, and normalization in order to prepare the dataset for predictive modeling.
###DATA PRE PROCESS
Data Preprocessing Pipeline Documentation
1. Overview

This project is designed to perform a comprehensive preprocessing workflow on a medical dataset.
The goal is to clean raw data and make it ready for machine learning models.

The implementation is built on top of the Scikit-Learn Pipeline architecture, ensuring that preprocessing steps are consistent and reproducible.

2. Libraries Used

pandas, numpy → Data manipulation

scikit-learn → Pipeline, preprocessing, train/test splitting

sys → Error handling

3. Main Classes and Functions
3.1 GuvenliEtiketleyici (Safe Label Encoder)

A custom transformer compatible with Scikit-Learn

Provides a safe version of LabelEncoder

Creates a separate encoder for each column

Unseen categories in the test set are encoded as -1

Missing values are replaced with "EKSİK_DEGER" before encoding

3.2 VeriOnIsleyici (Data Preprocessor)

The core class for loading, cleaning, and preprocessing raw data

Methods

veri_yukle()
Loads the Excel file and strips whitespace from column names

kapsamli_temizlik() (comprehensive cleaning)

Removes unnecessary columns (HastaNo, KanGrubu)

Handles missing values with appropriate strategies

UygulamaSuresi → Extracts minutes, fills missing with median

Alerji, KronikHastalik, UygulamaYerleri → Replaced with default values

Cinsiyet → Filled with mode (most frequent value)

Removes duplicate rows

pipeline_olustur_ve_calistir(target_column, test_size, random_state)

Splits data into features (X) and target (y)

For numerical columns

Missing values filled with median

Standardized with StandardScaler

For categorical columns

Missing values filled with a constant

Encoded with GuvenliEtiketleyici

Produces training and test datasets

veri_ozeti_goster(df, title)
Displays dataset shape and missing value summary

4. Workflow

Load the data

processor = VeriOnIsleyici("projectpus.xlsx")
processor.veri_yukle()


Show pre-cleaning summary

processor.veri_ozeti_goster(processor.orijinal_veri, "Pre-cleaning Data")


Clean the data

cleaned_data = processor.kapsamli_temizlik()


Show post-cleaning summary

processor.veri_ozeti_goster(cleaned_data, "Post-cleaning Data")


Run the preprocessing pipeline

X_train, X_test, y_train, y_test = processor.pipeline_olustur_ve_calistir(
    target_column="TedaviSuresi",
    test_size=0.2,
    random_state=42
)

5. Example Output
DATA PREPROCESSING PIPELINE STARTED
 Data loaded successfully. Shape: (350, 12)

 === PRE-CLEANING DATA ===
Shape: (350, 12)
Missing Values:
UygulamaSuresi     20
Cinsiyet            5
...

 Data cleaning in progress...
 Cleaning completed. Final shape: (340, 10)

 === POST-CLEANING DATA ===
 No missing values detected.
------------------------------

Pipeline executed successfully.

PIPELINE COMPLETED
========================================
RESULT SUMMARY
 Processed Training Data Shape: (272, 25)
 Processed Test Data Shape:    (68, 25)
 Training Target Count: 272
 Test Target Count:     68

 You can now train machine learning models:
   Usage: model.fit(X_train, y_train)

6. Conclusion

With this pipeline

Raw data is systematically cleaned

Missing values, duplicates, and categorical variables are handled safely

The process is reproducible and transparent

Final outputs can be fed directly into machine learning algorithms
